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
#### CEM Style of CSS generation
##### Markup

```html
<body class="use--theme-materialDesign">
	<div class="cmp_dialog p_lyt--fullsize is--visible">
		<h1 class="cmp_dialog__title"></h1>
		<button class="cmp_dialog__confirmBtn"> OK </button>
	</div>
</body>

```


##### Styles

```css
+Component(dialog) {

	width: 100px;
	
	+Entity(title) { 
		color: gray; 
	}	
	+Entity(confirmBtn) { 
		border: 1px black solid;
	}

}

+Component(cancelDialog, extends: dialogComponent) {
	
	+Entity(title, extends: 'dialogComponent.titleEntity') {
		color: red;
	}
	+Entity(cancelBtn, extends: 'dialogComponent.confirmBtnEntity') {
		border: 1px red solid;
	}

	+Property (lyt, 'fullsize') {
		width: 100%;
	}
	
}

+Modifier(MOD_USE, 'theme-materialDesign') {
	+Component(cancelDialog) {
		+Entity(title) {
			color: dark-red;
		}
		+Entity(confirmBtn) { 
			border: 1px dark-red solid;
		}
	}
}

```