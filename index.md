## Global API Description

Signature description

The request parameters are sorted and spliced ​​together in ascending dictionary order (the timestamp should also be added to verify the signature), and the string to be signed is generated. All parameters have values:


```markdown
Syntax highlighted code block

appKey=wehmslauewe&time=1594468475403&phone=13587690001&symbol=2

```

Generate the string to be signed & the private key parameters (agreed) to generate the final string to be signed. For example, the private key is: xsdlkfjs2234dskl32kjoj, splicing it at the end of the string, the generated string format is: All parameters have value:

```markdown

appKey=wehmslauewe&phone=13587690001&symbol=2&time=1594468475403&appSecretKey=xsdlkfjs2234dskl32kjoj One or more parameters have no value:

```

```markdown

appKey=wehmslauewe&phone=13587690001&symbol=2&email=&symbol=2&time=1594468475403&appSecretKey=xsdlkfjs2234dskl32kjoj

```

```markdown

Assign this value to the signature parameter signature, and then put the signature in the request header. Note: For the following parameters to sign, please note: please remove the invalid 0 in the incoming parameters, such as coin_amount = 100, please do not pass in 100.00 for signature verification, generate a signature for the parameters according to the signature rules, and compare it with the signature in the request header, If they are consistent, the signature is passed.

```

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/hkdcom22/HKD.com-Api-Doc/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
