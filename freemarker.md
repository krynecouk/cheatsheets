## White-space handling
- parse time (template) 
- runtime (output)

### Parse time (template)
- `<#ftl strip_whitespace='true'>`	: removes white-space around FTL tags
- `<#ftl strip_text='true'>`		: removes line break between FTL tags
- `<#t>`				: removes all leading and trailing white-space in this line
- `<#lt>`				: removes all leading white-space in this line
- `<#rt>`				: removes all trainling white-space in this line

### Runtime (output)
- `<#compress>..</#compress>`		: removes indentations, empty lines and repeated spaces/tabs of the output

## Sources 
[1]: [Apache Freemarker Manual](https://freemarker.apache.org/docs/index.html)
