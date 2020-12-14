---
title: o[wordpress] Gravity Forms
author: PipisCrew
date: 2016-02-01
categories: [php]
toc: true
---

reference - [https://premium.wpmudev.org/blog/10-top-quality-plugins-for-creating-custom-wordpress-forms/](https://premium.wpmudev.org/blog/10-top-quality-plugins-for-creating-custom-wordpress-forms/)
[http://codecanyon.net/item/gravity-forms-wpdb-mysql-connect/5968479](http://codecanyon.net/item/gravity-forms-wpdb-mysql-connect/5968479)

https://www.youtube.com/watch?v=PGIHJpyE98k

## Test Form Created!

![snap011](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap011.png)

> so whats going on @ dbase!?

these tables added!
![snap010](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap010.png)

**wp_rg_form**
![snap012](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap012.png)

**wp_rg_form_meta**
- schema - 
![snap013](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap013.png)

- data (as you see holds all field at longtext field) -
![snap014](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap014.png)

**wp_rg_lead_detail**
![snap015](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap015.png)

![snap016](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap016.png)

## Outdated 

3rd party JS validation for GravityForms - https://github.com/bhays/gravity-forms-javascript-validation
Display Gravity Form Error Messages in a JavaScript Popup - http://strangework.com/2011/09/30/how-to-display-gravity-form-error-messages-in-a-javascript-popup/

## Validate the user input at PHP side only!

```js
source - https://www.gravityhelp.com/documentation/article/gform_validation/

//merge this script under wp-content\themes\twentysixteen\functions.php
//where 1 is the ID of the form (check first picture^)
add_filter( 'gform_validation_1', 'custom_validation' );
function custom_validation( $validation_result ) {
    $form = $validation_result['form'];

    //supposing we don't want input 1 to be a value of 86
    if ( rgpost( 'input_1' ) == 86 ) {

        // set the form validation to false
        $validation_result['is_valid'] = false;

        //finding Field with ID of 1 and marking it as failed validation
        foreach( $form['fields'] as &$field ) {

            //NOTE: replace 1 with the field you would like to validate
            if ( $field->id == '1' ) {
                $field->failed_validation = true;
                $field->validation_message = 'This field is invalid!';
                break;
            }
        }

    }

    //Assign modified $form object back to the validation result
    $validation_result['form'] = $form;

	return validation_result; 
}
```

## Submit the forms via AJAX

set is required or validation - ![snap021](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap021-1.png)

enable AJAX - ![snap020](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap020-1.png)

end user got - ![snap023](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap023-1.png)

## Hooks

https://www.gravityhelp.com/documentation/category/hooks/

### Formidable Addon - is Better!

[https://formidablepro.com](https://formidablepro.com)

On #Gravity Forms# you cant tie the data on addon tables, I mean just with a quick tsql. On first look the <span style="color:red">Formidable</span>
-allows to add custom html + JS! on different parts of #page form#
-you can join 2 tables and you have the data!! lets dive in! >>>>>>>>>>>>>

![snap024](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap024-1.png)

each form field, has his own ID/key- ![snap025](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap025.png)

this away, enable us to make a map on other dbase to use the fields ID. 

we have the fields - ![snap028](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap028-1.png)
writing the quick query (each field must be joined!)
![snap033](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap033.png)

```js
select tieA.item_id, tieA.meta_value as fullname,tieB.meta_value as age from wp_frm_items 
left join wp_frm_item_metas as tieA on tieA.item_id=wp_frm_items.id and tieA.field_id=83
left join wp_frm_item_metas as tieB on tieB.item_id=wp_frm_items.id and tieB.field_id=84
--where tieA.meta_value is not null
--group by tieA.item_id, tieA.meta_value
```

we have the pure records entered by the user! no custom tables, no nothing!

![snap031](https://www.pipiscrew.com/wp-content/uploads/2016/01/snap031-1.png)

## Setting a dropdown value via querystring

[https://formidablepro.com/help-desk/setting-a-dropdown-value-via-querystring/](https://formidablepro.com/help-desk/setting-a-dropdown-value-via-querystring/)
[Dynamic Field not recognizing Dynamic Default Value](https://formidablepro.com/help-desk/dynamic-field-not-recognizing-dynamic-default-value/)
[Default Values](https://formidablepro.com/knowledgebase/field-options/using-dynamic-default-values-in-fields/)
[Dynamic Fields](https://formidablepro.com/knowledgebase/field-types/dynamic/#)

origin - http://www.pipiscrew.com/?p=3532 wordpress-gravity-forms