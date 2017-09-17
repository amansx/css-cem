# CEM - Component Entity Modifier for CSS


CEM is an extension of [BEM](http://getbem.com/introduction/) written in Stylus and is designed to aid in the process of scaling and maintaining css.

## How does it work?
#### Consider a Dialog box

```
    +----------------------------+
    |                            |
    |      DIALOG BOX TITLE      |
    |                            |
    |                            |
    |         +--------+         |
    |         |   OK   |         |
    |         +--------+         |
    +----------------------------+
```
#### CEM Style
##### Markup

```html
<body class="use--theme-materialDesign">
	<div class="cmp_dialog p_lyt--fullsize is--hidden">
		<h1 class="cmp_dialog__title"></h1>
		<button class="cmp_dialog__confirmBtn"> OK </button>
	</div>
</body>

```


##### Styles

```stylus
@import('cem');

+Component(dialog) {
	width: 100px;	
	+Entity(title) { 
		color: gray; 
	}	
	+Entity(confirmBtn) { 
		border: 1px black solid;
	}

}

+Component(cancelDialog) {
	+Entity(title, $extends: 'dialogComponent.titleEntity') {
		color: red;
	}
	+Entity(cancelBtn, $extends: 'dialogComponent.confirmBtnEntity') {
		border: 1px red solid;
	}

	+Property(lyt, 'fullsize') {
		width: 100%;
	}
}

+Modifier(MOD_BOOL, 'hidden') {
	display: none;
}

+Modifier(MOD_USE, 'theme-materialDesign') {
	+Component(cancelDialog) {
		+Entity(title) {
			color: crimson;
		}
		+Entity(confirmBtn) { 
			border: 1px crimson solid;
		}
	}
}
```


#### Generated CSS
```css
.cmp_dialog {
  width: 100px;
}
.cmp_dialog__title,
.cmp_cancelDialog__title {
  color: #808080;
}
.cmp_dialog__confirmBtn,
.cmp_cancelDialog__cancelBtn {
  border: 1px #000 solid;
}
.cmp_cancelDialog__title {
  color: #f00;
}
.cmp_cancelDialog__cancelBtn {
  border: 1px #f00 solid;
}
.cmp_cancelDialog.p_lyt--fullsize {
  width: 100%;
}
.is--hidden {
  display: none;
}
.use--theme-materialDesign .cmp_cancelDialog__title {
  color: #dc143c;
}
.use--theme-materialDesign .cmp_cancelDialog__confirmBtn {
  border: 1px #dc143c solid;
}
```