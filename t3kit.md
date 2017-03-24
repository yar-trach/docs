# CONSTANTS

>Setup                   :   "fileadmin/templates/Configuration/TypoScript/lib.fluidContent.setupts"

>PageTS                  :   "fileadmin/templates/Configuration/PageTS/FluidContent.pagets"

>Library folder          :   "typo3conf/ext/theme_t3kit/Configuration/TypoScript/Library/lib.fluidContent.setupts"

>Default elements folder :   "typo3/sysext/fluid_styled_content/Configuration/TypoScript/Static/setup.txt"





# Change viewport

>Add this lines to **Setup** 

```typoscript
page.meta >
page.meta {

    X-UA-Compatible = ie=edge
    X-UA-Compatible.httpEquivalent = 1
    viewport = width=device-width, initial-scale=1.0, maximum-scale=2.0

    mobile-web-app-capable = yes
    apple-mobile-web-app-capable = yes
    apple-mobile-web-app-status-bar-style = black
    format-detection = telephone=no

}
```





# Add fonts

>Add this lines to **Setup**

```typoscript
page.headerData.231 = TEXT 
page.headerData.231.value = <link href="https://fonts.googleapis.com/css?family=Roboto:400,500" rel="stylesheet">
```





# Overwrite fonts set

>To overwrite fonts you need to use **Add fonts** section, but instead **231** var use **186**





# Add custom layout/wrapper class to element

>* wrapper
>* layout
>* class

>options:

>* 1910 = layout
>* 365 = wrapper
>* 395 = aligning
>* 375 = margin-top
>* 385 = margin-bottom

>Add this lines to **Setup**

```typoscript
tt_content {
    imageTextLink {
        dataProcessing {
            1910 {
                classMappings {
                    1001 = colored-background _color-1
                    1002 = colored-background _color-2
                    1003 = colored-background _color-3
                }
            }
        }
    }
}
```

>Add this lines to **PageTS**

```typoscript
TCEFORM.tt_content.layout {
    types {
        imageTextLink {
            addItems {
                --div-- = ImageTextLink layouts:
                1001 = Colored background. Color-1
                1002 = Colored background. Color-2
                1003 = Colored background. Color-3
            }
        }
    }
}
```





# Adding custom wrappers for grid elements

>* grid
>* wrapper
>* class

```typoscript
tt_content {
    gridelements_pi1.20.10.setup.Adv1ColumnGrid.cObject {
        dataProcessing {
            365 {
                classMappings {
                    1001 = colored-background _color-1
                }
            }
        }
    }
}

TCEFORM.tt_content.wrapper {
    types {
        gridelements_pi1 {
            # Based on that the default items still exists.
            addItems {
                1001 = Colored background. Color-1
            }
        }
    }
}
```





# Add color picker

>To add color picker to element you need to create flex form.

>Structure of flex form will be next:

```
<T3DataStructure>
    <meta>
        <langDisable>1</langDisable>
    </meta>
    <sheets>
        <sDEF>
            <ROOT>
                <TCEforms>
                    <sheetTitle>LLL:EXT:theme_t3kit/Resources/Private/Language/ContentElements.xlf:iconTextButton.flexform.sheetGeneral</sheetTitle>
                </TCEforms>
                <type>array</type>
                <el>
                    <color>
                        <TCEforms>
                        <label>LLL:fileadmin/templates/theme_t3kit/custom_content_elements/Resources/Private/Language/CustomContentElements.xlf:nextButton.color</label>
                        <config>
                            <type>input</type>
                            <size>10</size>
                            <wizards>
                                <colorChoice>
                                    <type>colorbox</type>
                                    <title>color</title>
                                    <module>
                                        <name>wizard_colorpicker</name>
                                    </module> 
                                    <JSopenParams>height=600,width=380,status=0,menubar=0,scrollbars=1</JSopenParams>
                                </colorChoice>
                            </wizards>
                        </config>
                    </TCEforms>
                  </color>
                </el>
            </ROOT>
        </sDEF>
    </sheets>
</T3DataStructure>
```

>And add configs to **Setup**

```typoscript
20 = T3kit\T3kitExtensionTools\DataProcessing\FlexFormProcessor
20 {
    fieldName = pi_flexform
    as = settings
}
```





# Adding/updating templates and partials

>* partials
>* templates
>* layouts
>* header

>Add this to **Setup**

```typoscript
plugin.tx_themes {
    view {
        partialRootPaths {
            640 = fileadmin/templates/PROJECT_TITLE/Partials/
        }
        templateRootPaths{
            640 = fileadmin/templates/PROJECT_TITLE/Templates/
        }
        layoutRootPaths{
            640 = fileadmin/templates/PROJECT_TITLE/Layouts/
        }
    }
}
```

>or INLINE

```typoscript
plugin.tx_themes.view.partialRootPaths.640 = fileadmin/templates/PROJECT_TITLE/Partials
plugin.tx_themes.view.templateRootPaths.640 = fileadmin/templates/PROJECT_TITLE/Templates
plugin.tx_themes.view.layoutRootPaths.640 = fileadmin/templates/PROJECT_TITLE/Layouts
```

>Structure should be same like in t3kit_theme f.e.:

>/**PROJECT_TITLE**/Partials/Header/Header.html





# Adding layouts BE

>* layouts
>* BE

>Add this to **Setup**

```typoscript
plugin.tx_themes {
    view {
        layoutRootPaths{
            640 = fileadmin/templates/PROJECT_TITLE/Layouts/
        }
    }
}
```

>Add this lines to **Page TSConfig**

```typoscript
mod.web_layout.BackendLayouts {
    Nano {
        icon = EXT:theme_t3kit/Resources/Public/Icons/BackendLayouts/Content.svg
        name = Nano
        title = Nano
        config {
            backend_layout {
                colCount = 1
                rowCount = 2
                rows {
                    1 {
                        columns {
                            1 {
                                name = LLL:EXT:theme_t3kit/Resources/Private/Language/BackendLayouts.xlf:area_content
                                rowspan = 1
                                colPos = 0
                            }
                        }
                    }
                    2 {
                        columns {
                            1 {
                                name = LLL:EXT:theme_t3kit/Resources/Private/Language/BackendLayouts.xlf:area_elements
                                rowspan = 1
                                colPos = 4
                            }
                        }
                    }
                }
            }
        }
    }
}
```

>Create **Nano.html** in fileadmin/templates/**PROJECT_TITLE**/Layouts/

```html
<!-- theme_t3kit: Layouts/Nano.html [begin] -->
<f:render section="Default"/>
<!-- theme_t3kit: Layouts/Nano.html [end] -->
```

>Create fileadmin/templates/**PROJECT_TITLE**/Templates/Theme/ folder

>Create **Nano.html** here

```html
<div xmlns="http://www.w3.org/1999/xhtml" lang="en" xmlns:f="http://typo3.org/ns/fluid/ViewHelpers">
    <f:layout name="Nano" />
    <f:section name="Default">
    <!-- theme_t3kit: Templates/Theme/Nano.html [begin] -->

    <f:render partial="Content/Main" section="Default" arguments="{_all}" />

    <!-- theme_t3kit: Templates/Theme/Nano.html [end] -->
    </f:section>
</div>
```





# Adding templates for News extantion

>* news
>* templates

>Copy all templates to new folder and add custom templates /fileadmin/templates/News/Partials/List

>Add this lines to **Page TSConfig**

```typoscript
tx_news.templateLayouts {
    NewsCarousel = News carousel
    Cards  = News as Cards
    SimpleList = News as Simple List
    Timeline = News list with timeline
    AntroList = News Antroposofi List
}
```

>And this to **Setup**

```typoscript
plugin.tx_news.view.partialRootPaths.2 = fileadmin/templates/News/Partials/ 
```





# Setting elements to partials

>Add logo to header (custom place)

>Add wrapper to partial

```html
<div class="header-top__sub-logo">
    <f:cObject typoscriptObjectPath="lib.header.top.text" />
    <f:cObject typoscriptObjectPath="lib.header.top.logo" />
</div>
```

>Add settings to **Setup**

```typoscript
lib.header.top {
    logo = IMAGE
    logo.file = fileadmin/custom/images/nt-cargo-logo.svg
    logo.titleText = {$themes.configuration.siteName}
    logo.altText = {$themes.configuration.siteName}
    logo.params = class="header-top__sub-logo-img img-responsive"
    logo.stdWrap {
        required = 1
        typolink {
            parameter = 150
            parameter.insertData = 1
            title = {$themes.configuration.siteName}
            ATagParams = class="sub-class"
        }
    }
}
```





# Include custom.js

>custom.js is disabled by default, but it could be enabled if it needed

>Add this lines to **Setup**

```typoscript
page {
    includeJSFooter {
        customJs = fileadmin/custom/js/custom.js
        customJs {
            external = 0
            disableCompression =
            excludeFromConcatenation =
        }
    }
}
```





# Add custom.less CSS/LESS files to head

>* css
>* less
>* custom

>Add this lines to **Setup**

```typoscript
page {
    includeCSS {
        nanoCSS = fileadmin/custom/css/custom-nano.less
        nanoCSS {
            external = 0
            disableCompression =
            excludeFromConcatenation =
        }
    }
}
```





# Debugging

>* debug
>* setup

>Add this to **Setup** for debugging 

```typoscript
config.contentObjectExceptionHandler = 0
```





# Adding custom variables (constants)

>* custom
>* constants
>* variables
>* theme

>Add this to **Constants** (Root / Template)

```typoscript
themes.configuration.header.background = #f3ac24
```

>How to get constant:

>Use this constant with curly braces

```html
{theme:constant(constant:'themes.configuration.header.background')}
```





# Page TSConfig in file

>* TSConfig

>Add this to **Page TSConfig** and create file page.ts in this folder

```typoscript
<INCLUDE_TYPOSCRIPT: source="FILE:fileadmin/templates/PROJECT_TITLE/PageTS/page.ts">
```





# How to add/change language constants

>* constants
>* language
>* setup

>Add this to **Setup**

```typoscript
plugin.tx_extname {
    _LOCAL_LANG.DEFAULT {
        someConstant = some value
    }
}
```

Example

```typoscript
plugin.tx_pxanewslettersubscription {
    _LOCAL_LANG.da {
        subscribe = Tilmeld
    }
}
```




# Fluid variables

>* var
>* custom
>* fluid

>Add this to template/partial (html)

```html
<v:variable.set name="count" value="{product.attributeValues -> f:count()}" />
<f:if condition="{settings.includeSkuInAttributeListing}">
    <f:then>
        <v:variable.set name="fullCount" value="{v:math.sum(a: count, fail: 0, b: 1)}" />
        <v:variable.set name="halfCount" value="{v:math.division(a: fullCount, fail: 0, b: 2)}" />
        <v:variable.set name="halfCount" value="{v:math.ceil(a: halfCount, fail: 0)}" />
        <v:variable.set name="halfCount" value="{v:math.subtract(a: halfCount, fail: 0, b: 1)}" />
    </f:then>
    <f:else>
        <v:variable.set name="fullCount" value="{count}" />
        <v:variable.set name="halfCount" value="{v:math.division(a: fullCount, fail: 0, b: 2)}" />
        <v:variable.set name="halfCount" value="{v:math.ceil(a: halfCount, fail: 0)}" />
    </f:else>
</f:if>
<v:variable.set name="mod" value="{v:math.modulo(a: fullCount, b: 2)}" />
<f:if condition="{mod} != 0">
    <v:variable.set name="addLine" value="1" />
</f:if>
```

>Use "addLine" variable later

```html
<f:if condition="{addLine}">
    <tr><th>&nbsp;</th><td></td></tr>
</f:if>
```





# HTACCESS redirects

>* htaccess
>* redirects

>http://htaccess.madewithlove.be/

```htaccess
RewriteCond %{HTTP_HOST} ^(www\.)?meda.dk$
RewriteCond %{REQUEST_URI} ^/sundhedspersonale/
RewriteRule ^(.*)$ http://www.medainfo.dk/$1 [R=301,L]

RewriteCond %{HTTP_HOST} ^(www\.)?medainfo.dk$
RewriteCond %{REQUEST_URI} ^/forbruger/
RewriteRule ^(.*)$ http://www.meda.dk/$1 [R=301,L]

RewriteCond %{HTTP_HOST} fr.naloc.be [NC]
RewriteCond %{REQUEST_URI} ^/$
Rewriterule ^(.*)$ http://www.naloc.be/fr/ [L,R=301]

~~~~~ redirect from just main page to some subpage ~~~~~
RewriteCond %{HTTP_HOST} ^(www\.)?intimhalsa.se$
RewriteCond %{REQUEST_URI} ^/$                 
RewriteRule ^(.*)$ http://www.intimhalsa.se/erektion/ [R=301,L]

~~~~~ redirect just one subpage to another domain subpage ~~~~~
RewriteCond %{HTTP_HOST} ^(www\.)?epipenuk.meda-core.local$
RewriteCond %{REQUEST_URI} ^/patients/$
RewriteRule ^(.*)$ http://www.intimhalsa.se/erektion/ [R=301,L]

~~~~~ redirect single page with same name to another domain, regex ~~~~~
RewriteCond %{HTTP_HOST} ^(www\.)?epipenuk.meda-core.local$
RewriteCond %{REQUEST_URI} ^/patients/?$
RewriteRule ^(.*)$ http://www.intimhalsa.se/$1 [R=301,L]

~~~~~ redirect all subpages ~~~~~
RewriteCond %{HTTP_HOST} ^(www\.)?epipenuk.meda-core.local$
RewriteCond %{REQUEST_URI} ^/patients/(.*)$
RewriteRule ^(.*)$ http://www.intimhalsa.se/patients/ [R=301,L]
```





# How to check redirects locally

>Add sending domain locally 

>Ping new site

```console
$ ping se.triolab.typo3konsult.se
```

>Get it IP address

>Result:

```console
64 bytes from c2938.cloudnet.se (139.162.190.251): icmp_seq=3 ttl=56 time=42.8 ms

139.162.190.251
```

>Go do /etc/hosts file and add this IP to hosts list

```console
139.162.190.251 triolab.se
```

>Now it will work locally





# Adding language variables

>* language
>* variable
>* typoscript
>* setup

>Add this to **Setup**, where "**L**" is ID of language.

>Lang ID you can find in "List" 

>Default lang

```typoscript
page.10.variables {
    header_text = TEXT
    header_text {
        value = -En del av Addtech koncernen
        #value = -A PART OF ADDTECH GROUP
        wrap = <div class="head-middle-text">|</div>
        typolink.parameter = http://www.addtech.com/
        typolink.wrap = <p>|</p>
        typolink.ATagBeforeWrap = 1
        typolink.extTarget = _blank
    }
}
```

```typoscript
# Lang with ID = 1 (English)
[globalVar = GP:L = 1]
# pixelant.footer.contact.title = العنوان البريدي.
# pixelant.footer.contact.bar.title = الزائرين.
# pixelant.footer.contact.bar.address = Pipers väg 2A,

page.10.variables {
    header_text = TEXT
    header_text {
        #value = -En del av Addtech koncernen
        value = -A PART OF ADDTECH GROUP
        wrap = <div class="head-middle-text">|</div>
        typolink.parameter = http://www.addtech.com/
        typolink.wrap = <p>|</p>
        typolink.ATagBeforeWrap = 1
        typolink.extTarget = _blank
    }
}

[global]
```





# Change template of element with TypoScript

>* footer
>* elements
>* TS

>Add this lines to **Setup**

```typoscript
lib.footer.copyright = TEXT
lib.footer.copyright {
    data = date:U
    strftime = %Y
    noTrimWrap= |<p class="copyright"> © | {$themes.configuration.footer.copyright}</p>|
}
```





# How to translate 'Read more' button

>* lang
>* translation
>* setup

>Add this to **Setup**

```typoscript
plugin.tx_theme_t3kit._LOCAL_LANG.sv.contentElement.slider.linkText = Läs mer
```





# Add custom classes to links in RTE

>* custom
>* class
>* RTE

>Add this to **Page TSConfig**

```typoscript
RTE.default.proc.allowedClasses := addToList(btn-border, btn-primary-background)
RTE.default.buttons.link.properties.class.allowedClasses := addToList(btn-border, btn-primary-background)
RTE.classes.btn-border.name = Button with border
RTE.classes.btn-primary-background.name = Primary Button
```

>OR

```typoscript
RTE.default{
    ignoreMainStyleOverride = 1 
    useCSS = 1
    showTagFreeClasses = 1
    contentCSS = fileadmin/templates/css/rte.css
    buttons {
        blockstyle.tags.div.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
        blockstyle.tags.p.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
        formatblock.tags.div.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
        formatblock.tags.p.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
        textstyle.tags.span.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
        link.properties.class.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
    }
    proc.allowedClasses := addToList(youtube-vintage, fb-vintage, www-vintage)
}
```

>OR

```typoscript
RTE {
    default {
        proc.allowedClasses >
        proc.allowedClasses = btn, btn-default, infoRow
        buttons {
            blockstyle.tags {
                div.allowedClasses = btn, btn-default, infoRow
            }
            textstyle.tags {
                span.allowedClasses = btn, btn-default
            }
        }
        contentCSS = fileadmin/templates/rte.css
        showTagFreeClasses = 0
        enableWordClean = 1
        useCSS = 0
    }
}

RTE.default.FE < RTE.default
RTE.default.FE.FE >
RTE.config.tt_content.bodytext
RTE.config.tt_content.bodytext.proc.allowedClasses = btn, btn-default, infoRow
```





# Add second link to element

>* flexform
>* link

>Add to/create flexform for element you want to add custom (second) link

```xml
<link2>
    <TCEforms>
        <label>Link</label>
        <config>
            <type>input</type>
            <eval>trim</eval>
            <size>60</size>
            <default></default>
            <wizards type="array">
                <_PADDING type="integer">2</_PADDING>
                <link type="array">
                    <type>popup</type>
                    <title>Link</title>
                    <icon>link_popup.gif</icon>
                    <module type="array">
                        <name>wizard_element_browser</name>
                        <urlParameters type="array">
                            <mode>wizard</mode>
                            <act>file</act>
                        </urlParameters>
                    </module>
                    <JSopenParams>height=500,width=500,status=0,menubar=0,scrollbars=1</JSopenParams>
                </link>
            </wizards>                
        </config>
    </TCEforms>
</link2>
```

>You will get 'link2' var with link





# Google analiticts

>* google
>* analiticts
>* Setup

>Add this to **Setup**

```typoscript
page.headerData.5364 = TEXT
page.headerData.5364.value (
    <script type="text/javascript">
        var _gaq = _gaq || [];
        _gaq.push(['_setAccount', 'UA-999999-9']);
        _gaq.push(['_trackPageview']);
        (function() {
        var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
        ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
        var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
        })();
    </script>
)
```





# Change template of content element

>* template

>Add this lines to **Setup**

```typoscript
plugin.tx_themes.view.templateRootPaths.700 = fileadmin/templates/theme_t3kit/override/
lib.fluidContent.templateRootPaths.1913 = fileadmin/templates/theme_t3kit/override/ContentElements
```





# Change classes for table template

>* table
>* setup

>Add this to **Setup**

```typoscript
lib.parseFunc_RTE {
    externalBlocks {
        table.stdWrap.HTMLparser.tags.table.fixAttrib.class {
            default = table table-hover
            always = 1
            list >
        }
    }
}
```





# Overriding template for element by selector

>* constants
>* Setup

>Add constant variable to **Constants**

```typoscript
themes.configuration.features.companySelector = 632
```

>Add TypoScript to **Setup** for overriding

```typoscript
lib.menu.main {
    1 {
        NO {
            wrapItemAndSub.override = <li class="main-navigation__item _contacts js__main-navigation__item uid-{field:uid} point-{register:count_MENUOBJ} first">|</li>|*|<li class="main-navigation__item js__main-navigation__item _contacts uid-{field:uid} point-{register:count_MENUOBJ} middle">|</li>|*|<li class="main-navigation__item _contacts js__main-navigation__item uid-{field:uid} point-{register:count_MENUOBJ} last">|</li>
            wrapItemAndSub.override.if {
                value.data = field:uid
                isInList = {$themes.configuration.features.contactsUid}
            }
        }
        ACT {
            wrapItemAndSub.override = <li class="main-navigation__item _contacts js__main-navigation__item _active uid-{field:uid} point-{register:count_MENUOBJ} first">|</li>|*|<li class="main-navigation__item _contacts js__main-navigation__item _active uid-{field:uid} point-{register:count_MENUOBJ} middle">|</li>|*|<li class="main-navigation__item _contacts js__main-navigation__item _active uid-{field:uid} point-{register:count_MENUOBJ} last">|</li>
            wrapItemAndSub.override.if {
                value.data = field:uid
                isInList = {$themes.configuration.features.contactsUid}
            }
        }
        IFSUB {
            wrapItemAndSub.override = <li class="main-navigation__item _contacts _list {$themes.configuration.menu.main.dropdown} uid-{field:uid} point-{register:count_MENUOBJ} first">|</li>|*|<li class="main-navigation__item _contacts _list {$themes.configuration.menu.main.dropdown} uid-{field:uid} point-{register:count_MENUOBJ} middle">|</li>|*|<li class="main-navigation__item _contacts _list {$themes.configuration.menu.main.dropdown} uid-{field:uid} point-{register:count_MENUOBJ} last">|</li>
            wrapItemAndSub.override.if {
                value.data = field:uid
                isInList = {$themes.configuration.features.contactsUid}
            }
            ATagParams = class="main-navigation__item-link js__main-navigation__item-link"
            after = <a href="#" class="main-navigation__open-sub-menu-link js__main-navigation__open-sub-menu-link">Open</a>
        }
    }
}
```





# Overriding default language menu

>Add this to **Setup**

```typoscript
lib.fluidContent.templateRootPaths.1920 = fileadmin/templates/theme_t3kit/Resources/Private/Templates/FluidStyledContent
```

>Add this to **Constants**

```typoscript
lib.menu.language.standard.templateName = LanguageMenuDropdown
```

>Create **LanguageMenuDropdown.html** file with template located:

>./templates/theme_t3kit/Resources/Private/Templates/FluidStyledContent/**LanguageMenuDropdown.html**

```html
<f:if condition="{languages}">
    <div class="header-top__language-menu">
        <f:for each="{languages}" as="language">
            <f:if condition="{language.active}">
                <a class="header-top__language-menu-btn js__header-top__language-menu-btn" href="/#"><span class="main-flag-icon flag-icon flag-icon-globe"></span><span class="flag-language">{language.languageIsocode}</span><span class="icons icon-arrow-down"></span> </a>
            </f:if>
        </f:for>
        <div class="header-top__language-menu-box js__header-top__language-menu-box">
            <f:for each="{languages}" as="language">
                <f:link.page addQueryString="1"
                  additionalParams="{L: language.L}"
                  title="{language.label}"
                  class="header-top__language-menu-box-item{f:if(condition: language.active, then: ' active')}"
                  argumentsToBeExcludedFromQueryString="{0: 'id'}">
                    <span class="flag-icon"></span> {language.languageIsocode}
                </f:link.page>
            </f:for>
            <a class="header-top__language-menu-box-close-btn js__header-top__language-menu-box-close-btn"></a>
        </div>
    </div>
</f:if>
```