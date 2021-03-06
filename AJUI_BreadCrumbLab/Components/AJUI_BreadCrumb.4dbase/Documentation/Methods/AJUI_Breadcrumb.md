﻿<!--   AJUI_Breadcrumb.new ( {template} ) -> instance of Breadcrumb class  -->


## Description

Exposes the Breadcrumb class at the host base. Replace New AJUI_BreadCrumb since V18R3. It is possible to pass an object as a parameter to it in order to import an AJUI Breadcrumb template (JSON file). 

```4d
  AJUI_Breadcrumb.new ( {template} ) -> instance
```

| Parameter | Type | In/Out | Description |
| --------- | ---- | ------ | ----------- |
| template | object | in | Properties :<br> - (text) templateName :  Name of the folder containing the JSON file to import (template). If the file is not found, the method will return a new instance of AJUI BreadCrumb.<br> - (text) (optional) templatePath : You can specify a path to retrieve the file otherwise, the component will search in the default folder located in the resources (.../Resources/AJUI_BreadCrumb_Templates/). |
| instance | object | out | instance of AJUI_BreadCrumb with all the member functions |

## Example

```4d

 //Import template and add callback with params from the lab (HDI groupedButtons)
  Case of 
	: (Form event code=On Load)
		C_OBJECT($bc)
		$bc:=New object()
		$bc.templateName:="groupedBtn_selection.json"
		
		Form.bc1:=AJUI_BreadCrumb.new ($bc)
		Form.bc1.Name("bc1")
		
		  //add callback
		$section_obj:=New object
		$section_obj.onClickCB:="HDI_setNote"
		$params:=New object
		$params.notationNB:=1
		For ($i;1;5)
			$params.note:=$i
			$section_obj.onClickCBParams:=OB Copy($params)
			Form.bc1.UpdateSection("note"+String($i);$section_obj)
		End for 
		
 End case 

 Form.bc1.Draw()
```
