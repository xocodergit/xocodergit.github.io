## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/xocodergit/xocodergit.github.io/edit/main/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/xocodergit/xocodergit.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.

```go
func StructPatch(dest interface{}, patch interface{}) error {
	destObjMeta := reflect.ValueOf(dest)
	if !strings.HasPrefix(destObjMeta.Type().String(), "*") {
		return errors.New("invalid type of dest, it must be a pointer")
	}

	patchObjMeta := reflect.ValueOf(patch)
	if strings.HasPrefix(patchObjMeta.Type().String(), "*") {
		return errors.New("invalid type of patch, it must not be a pointer")
	}

	for i := 0; i < patchObjMeta.NumField(); i++ {
		vtype := patchObjMeta.Field(i).Type()
		if !strings.HasPrefix(vtype.String(), "*") {
			// skip the none pointer field
			continue
		}
		if patchObjMeta.Field(i).IsNil() {
			continue
		}
		destObjMeta.Elem().Field(i).Set(patchObjMeta.Field(i))
	}
	return nil
}
```
