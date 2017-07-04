# Add Indentation and Frames

>Add this to **Page TS**

```TypoScript
TCEFORM.tt_content.section_frame {
	addItems.108 = Video player container
}
```

>Add this to **Setup**

```TypoScript
tt_content.stdWrap.innerWrap.cObject.108 < tt_content.stdWrap.innerWrap.cObject.default
tt_content.stdWrap.innerWrap.cObject.108 {
	20.10.value = csc-default
	30.cObject.default.value = ><div class="video-player-container">|</div></div>
 	#30.cObject.menu.value = >|</div>
}
```




# Add icons to Accordion

>Add this to **template of Accordion**

```TypoScript
<flux:field.userFunc name="icon" userFunc="Pixelant\PxaGenericContent\UserFunction\DynamicIcons->renderField" default="" />
```

>And render icon like this

```TypoScript
<f:if condition="{icon}">
  <span class="icons icon-{icon}"></span>
</f:if>
```
