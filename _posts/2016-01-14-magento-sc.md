---
title: Magento script export products to XML for Skroutz
author: PipisCrew
date: 2016-01-14
categories: [php]
toc: true
---

reference - [https://developer.skroutz.gr/el/feedspec/](https://developer.skroutz.gr/el/feedspec/)

```js
//test.php
<?php error_reporting(e_all="" |="" e_strict);="" define('magento_root',="" getcwd());="" $compilerconfig="MAGENTO_ROOT" .="" '/includes/config.php';="" if="" (file_exists($compilerconfig))="" {="" include="" $compilerconfig;="" }="" $magefilename="MAGENTO_ROOT" .="" '/app/mage.php';="" require_once="" $magefilename;="" ini_set('display_errors',="" 1);="" mage::app();="" $storeid="1;" the="" store="" id="" for="" the="" export="" mage::app()-=""?>setCurrentStore(Mage::getModel('core/store')->load($storeId));
$collection = Mage::getModel('catalog/product')->getCollection();
$collection->addAttributeToSelect('*');
$collection->addAttributeToFilter('status', 1);//only active products
//$lines = array();

//Set Greek Timezone
date_default_timezone_set('Europe/Athens');
$today = date("Y.m.d H:m"); 

//Create the XML element
$xml = new SimpleXMLElement('<?xml version="1.0" encoding="UTF-8"?><xml></xml>');

$product = $xml->addChild('mywebstore');

$xml = new DOMDocument();
$mystore = $xml->createElement( 'mywebstore' );

$created = $xml->createElement( 'created_at' );
$created->nodeValue = $today;
$mystore->appendChild( $created ); 

$products = $xml->createElement( 'products' );

//each product on one line:
foreach ($collection as $_product) {

	$skus = array("TBGC1.1","TBGC1.2","TBGC2.1","TBGC2.2","TBGC3.1","TBGC3.2","TBGC4.1","TBGC4.2","TBGC5.1","TBGC5.2","TBGC6.1","TBGC6.2","TBGC7.1","TBGC7.2","TBGC8.1","TBGC8.2","TBGC9.2","TBBC1","TBBC2","MDPC1.1","MDPC2.1","MDPC3.1","MDPC4.1","MDPC1","MDPC2","MDPC3","MDPC4","OB_C1.1","OB_C1.2","OB_C2.1","OB_C2.2","TBNC1.1","TBNC1.2","TBNC2.1","TBNC2.2","TBNC3.1","TBNC3.2","TBNC4.1","TBNC4.2","TBNC5.1","TBNC5.2","TBNC6.1","TBNC6.2","TBNC7.1","TBNC7.2","TBNC8.1","TBNC8.2","TBNC9.1","T","NC9.2","TBNC10.1","TBNC10.2","MDEG1","AGEG1","MDFG1","MDFG2","MD_P1","MD_P2","AG_P1","AG_P2","AG_P3");

	if(in_array($_product->getSku(), $skus)){
		//Create Product Node
		$product = $xml->createElement( 'product' );

		//Add Product SKU
		$id = $xml->createElement( 'id' );
		$id->nodeValue = $_product->getSku();

		//Add Product Name
		$name = $xml->createElement( 'name' );
		$cdataname = $xml->createCDATASection($_product->getName());
		$name->appendChild($cdataname);

		//Add Product Link
		$string = $_product->getProductUrl();
		$productlink = strip_html_tags($string);
		$link = $xml->createElement( 'link' );
		$cdatalink = $xml->createCDATASection($productlink);
		$link->appendChild($cdatalink);

		//Add Product Image
		$product_image = Mage::helper('catalog/image')->init($_product, 'image')->__toString();
		$image = $xml->createElement( 'image' );
		$cdataimage = $xml->createCDATASection($product_image);
		$image->appendChild($cdataimage);

		//Add Category Name
		$categoryIds = $_product->getCategoryIds();

		$category = Mage::getModel('catalog/category');
		$tree = $category->getTreeModel();
		$tree->load();

		$productids = $tree->getCollection()->getAllIds();
		$categories = array();
		if ($productids)
		{
			foreach ($productids as $productid)
			{
				$category->load($productid);
				$categories[$productid]['name'] = $category->getName();
				$categories[$productid]['path'] = $category->getPath();
			}
			foreach ($productids as $productid)
			{
				$path = explode('/', $categories[$productid]['path']);
				$string = '';
				foreach ($path as $pathId)
				{
					$string.= $categories[$pathId]['name'] . ' > ';
					$cnt++;
				}
				$category_path = substr($string, 0, -3);
			}
		}

        if(count($categoryIds) ){
            $firstCategoryId = $categoryIds[0];
            $_category = Mage::getModel('catalog/category')->load($firstCategoryId);
			$category = $xml->createElement( 'category' );
			$cdatacategory = $xml->createCDATASection($category_path);
			$category->appendChild($cdatacategory);
        }

		//Add Product Price
		$price = $xml->createElement( 'price_with_vat' );
		$price->nodeValue = number_format($_product->getFinalPrice(), 2, '.', '');;

		//Add Manufacturer
		$manufacturer = $xml->createElement( 'manufacturer' );
		$cdatamanufacturer = $xml->createCDATASection($_product->getAttributeText('marka'));
		$manufacturer->appendChild($cdatamanufacturer);

		//Add Description
		$str = $_product->getShortDescription();
		$result = strip_html_tags($str);
		$description = $xml->createElement( 'description' );
		$cdatadescription = $xml->createCDATASection($result);
		$description->appendChild($cdatadescription);

		//Add Stock Availability
		$stockStatus = $_product->getAvailability();
		if ($stockStatus = 'instock'){
		$availability = $xml->createElement( 'availability' );
		$cdataavailability = $xml->createCDATASection('Σε απόθεμα - Παράδοση σε 1-2 ημέρα');
		$availability->appendChild($cdataavailability);
		$instock =  $xml->createElement( 'instock' );
		$instock->nodeValue = 'Y';
		}
		else {
		$availability = $xml->createElement( 'availability' );
		$cdataavailability = $xml->createCDATASection('Κατόπιν Παραγγελίας');
		$availability->appendChild($cdataavailability);
		$instock =  $xml->createElement( 'instock' );
		$instock->nodeValue = 'N';
		}

		//Add all node in product element
		$product->appendChild( $id ); 
		$product->appendChild( $name); 
		$product->appendChild( $link ); 
		$product->appendChild( $image ); 
		$product->appendChild( $category ); 
		$product->appendChild( $price ); 
		$product->appendChild( $manufacturer ); 
		$product->appendChild( $description ); 
		$product->appendChild( $availability );
		$product->appendChild( $instock );
	}
	//Add Product in Feed
	$products->appendChild( $product ); 
}
//end loop
$mystore->appendChild( $products );
$xml->appendChild( $mystore );
$xml->formatOutput = true; // set the formatOutput attribute of domDocument to true
$xml->save("skroutz.xml");

print_r("Successful Createion of XML!");
?>

<?php ------------------------------------="" function="" strip_html_tags($string)="" {="" $string="str_replace("\r"," '="" ',="" $string);="" $string="str_replace("\n"," '="" ',="" $string);="" $string="str_replace("\t"," '="" ',="" $string);="" $string="str_replace(" "," '="" ',="" $string);="" $string="str_replace("&"," '&',="" $string);="" $pattern='/<[^>]*>/' ;="" $string="preg_replace" ($pattern,="" '="" ',="" $string);="" $string="trim(preg_replace('/" {2,}/',="" '="" ',="" $string));="" return="" $string;="" }="" ------------------------------------=""?>
```

origin - http://www.pipiscrew.com/?p=3205 magento-script-export-products-to-xml-for-skroutz