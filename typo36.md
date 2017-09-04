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





# Add images to Tabs

```TypoScript
{namespace v=Tx_Vhs_ViewHelpers}
{namespace flux=FluidTYPO3\Flux\ViewHelpers}

<f:layout name="Content" />

<div xmlns="http://www.w3.org/1999/xhtml"
	 xmlns:v="http://fedext.net/ns/vhs/ViewHelpers"
	 xmlns:flux="http://fedext.net/ns/flux/ViewHelpers"
	 xmlns:f="http://typo3.org/ns/fluid/ViewHelpers">

<f:section name="Configuration">
	<flux:form
		 wizardTab="smk-generic-content-special"
		 id="smktabs"
		 icon="{v:extension.path.resources(path: 'Icons/pxa.gif')}">

		<flux:form.sheet name="display">
			<flux:field.select name="mode" items="tab,pill" />
			<flux:field.select name="position" items="default,pull-left,pull-right" />
		</flux:form.sheet>

		<f:comment><!-- Make sure record is saved before adding children --></f:comment>
		<f:if condition="{record.uid} > 0">
			<f:then>
				<flux:form.sheet name="children">
					<flux:form.section name="children">
						<flux:form.object name="child">
							<flux:field.input name="title" />
							<flux:field.input name="class" />
							<flux:field.checkbox name="active" />
							<flux:field.checkbox name="fade" />
							<flux:flexform.field.file name="image" label="Preview image" allowed="jpg,png,gif" />
						</flux:form.object>
					</flux:form.section>
				</flux:form.sheet>
			</f:then>
			<f:else>
				<flux:form.sheet name="saveFirst">
				</flux:form.sheet>
			</f:else>
		</f:if>

		<flux:grid>
			<flux:grid.row>
				<f:if condition="{children}">
					<f:for each="{children}" as="child" iteration="iteration">
						<flux:grid.column name="{child.child.id}" label="{f:if(condition: child.child.title, then: child.child.title, else: 'Tab {iteration.cycle}')}" style="width: {v:math.division(b: '{children -> f:count()}', a: 100)}%">
							<flux:form.content name="{child.child.id}" />
						</flux:grid.column>
					</f:for>
				</f:if>
			</flux:grid.row>
		</flux:grid>
	</flux:form>
</f:section>

<f:section name="Preview">
	<flux:widget.grid />
</f:section>

<f:section name="Main">
	<v:var.set name="activeTabIndex" value="0" />
	<f:if condition="{children}">
		<f:for each="{children}" as="child" iteration="iteration">
			<f:if condition="{child.child.active}">
				<v:var.set name="activeTabIndex" value="{iteration.index}" />
			</f:if>
		</f:for>
	</f:if>

	<div class="tabbable _preview">
		<f:render section="Tabs" arguments="{_all}" />

		<div class="tab-content">
			<f:if condition="{children}">
				<f:for each="{children}" as="child" iteration="iteration">
					<div class="tab-pane {f:if(condition: child.child.fade, then: 'fade')} {f:if(condition: '{activeTabIndex} == {iteration.index}', then: 'active in')} {f:if(condition: child.child.class, then: 'tab-pane-{child.child.class}')}" id="tab-{record.uid}-{iteration.index}">
						<flux:content.render area="{child.child.id}" />
					</div>
				</f:for>
			</f:if>
		</div>

		<f:if condition="{0: tabDirection} == {0: 'below'}">
			<f:render section="Tabs" arguments="{_all}" />
		</f:if>
	</div>
</f:section>

<f:section name="Tabs">
	<f:if condition="{children}">
		<ul class="nav nav-{mode}s {position}">
			<f:for each="{children}" as="child" iteration="iteration">
				<li class="nav-link {f:if(condition: '{activeTabIndex} == {iteration.index}', then: 'active')} {f:if(condition: child.child.class, then: 'tab-{child.child.class}')}">
					<a href="{v:page.absoluteUrl()}#tab-{record.uid}-{iteration.index}" data-toggle="{mode}">
						<figure class="image">
							<f:image src="{child.child.image}" minWidth="110" />
							<figcaption><f:format.raw>{child.child.title}</f:format.raw></figcaption>
						</figure>
					</a>
				</li>
			</f:for>
		</ul>
	</f:if>
</f:section>

</div>

```

> To add input (section Configuration):

```TypoScript
<flux:flexform.field.file name="image" label="Preview image" allowed="jpg,png,gif" />
```

> Render image (section Tabs):

```TypoScript
<f:image src="{child.child.image}" minWidth="110" />
```
