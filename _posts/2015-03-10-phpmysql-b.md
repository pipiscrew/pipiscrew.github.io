---
title: o[php+mysql] batch export invoices (each as docx) and download them as zip file!
author: PipisCrew
date: 2015-03-10
categories: []
toc: true
---

reference
[http://www.phpclasses.org/package/8247-PHP-Create-Microsoft-Word-documents-from-templates.html](http://www.phpclasses.org/package/8247-PHP-Create-Microsoft-Word-documents-from-templates.html)
class - [http://pastebin.com/kyp4vVH2](http://pastebin.com/kyp4vVH2)

```js
//index.php
<?php require_once="" ('config.php');="" include('docxtemplate.class.php');="" connect="" $db="connect();" get="" recordset="" $s="getSet($db," select"="" *="" from="" offers="" where="" invoice_sent_when="" between="" '2013-01-01'="" and="" '2016-01-01'",null);="" if="" (!$s){="" die("no="" records="" found="" for="" this="" period");="" }="" $dt="date(" ymd_his");"="" create="" dir="" for="" today="" mkdir("./{$dt}",="" 0700);="" foreach($s="" as="" $row)="" {="" for="" each="" record="" generate="" a="" docx="" into="" created="" dir="" if="" (!generate_docx($db,="" $row,"./{$dt}/"))="" {="" echo="" "error!";="" exit;="" }="" }="" compress="" the="" created="" dir="" (includes="" all="" docx)="" $filename="{$dt}.zip" ;="" $zip="new" zipper;="" $zip-=""?>open($filename,Zipper::CREATE);
$zip->addDir($dt,$dt);
$zip->close();

if(!file_exists($filename)){
	//if file zipped correctly
	die("File doesnt exist");
}

/////////////////////////////////// SEND ZIPPED FOLDER TO USER
$filepath = getcwd()."/";

// http headers for zip downloads
header("Pragma: public");
header("Expires: 0");
header("Cache-Control: must-revalidate, post-check=0, pre-check=0");
header("Cache-Control: public");
header("Content-Description: File Transfer");
header("Content-type: application/octet-stream");
header("Content-Disposition: attachment; filename=\"".$filename."\"");
header("Content-Transfer-Encoding: binary");
header("Content-Length: ".filesize($filepath.$filename));
ob_end_flush();
@readfile($filepath.$filename);

/////////////////////////////////// DELETE TEMPORARY FOLDER + ZIP
//delete the created zip file
unlink($filename);

//delete the folder
recursiveRemove("./{$dt}/");

function recursiveRemove($dir) {
    $structure = glob(rtrim($dir, "/").'/*');
    if (is_array($structure)) {
        foreach($structure as $file) {
            if (is_dir($file)) recursiveRemove($file);
            elseif (is_file($file)) unlink($file);
        }
    }
    rmdir($dir);
}

function generate_docx($db, $row, $folder)
{

	$docx = new DOCXTemplate('template_invoice.docx');
	$docx->set('seller', $row['offer_seller_name']);
	$docx->set('comp_name', $row['offer_company_name']);

	$prop_date = date_create_from_format('Y-m-d', $row['offer_proposal_date']);

	$docx->set('pdate', date_format($prop_date, 'd-m-Y'));
	$docx->set('period', $row['offer_contract_period']);

	$invoice_details = getRow($db,"select client_invoice_detail_id, client_id, company_name, occupation, address, pobox, city, countries.country_name as country_id, vat_no, tax_offices.tax_office_name as tax_office_id from client_invoice_details
 left join tax_offices on tax_offices.tax_office_id = client_invoice_details.tax_office_id
 left join countries on countries.country_id = client_invoice_details.country_id
 where client_invoice_detail_id=?",array($row['invoice_detail_id']));

	//invoice details
	$docx->set('comp_tax_name', $invoice_details['company_name']);
	$docx->set('comp_tax_subject', $invoice_details['occupation']);
	$docx->set('tax_afm', $invoice_details['vat_no']);
	$docx->set('tax_office', $invoice_details['tax_office_id']);
	$docx->set('country',  $invoice_details['country_id']);
	$docx->set('comp_address', $invoice_details['address']);

	$docx->set('srv_start',date_format($srv_start, 'd-m-Y'));
	$docx->set('srv_end', date_format($srv_end, 'd-m-Y'));
	$docx->set('fb_page', $row['offer_page_url']);
	$docx->set('comp_tel',  $row['offer_telephone']);
	$docx->set('no', $row['offer_no']);
	$docx->set('app', $row['offer_apps']);
	$docx->set('page', $row['gen_page']);
	$docx->set('fee',  add_thousand($row['gen_a_fee'],2));
	$docx->set('budget',  add_thousand($row['gen_a_budget'],2));

	return	$docx->saveAs($folder . $row["offer_no"] . '.docx'); 
}

function add_thousand($val, $decimal)
{
	return number_format( $val , $decimal , ',' , '.' );
}

class Zipper extends ZipArchive
{
	public function addDir($path, $parent_dir = '')
	{
		if($parent_dir != '')
		{
			$this->addEmptyDir($parent_dir);
			$parent_dir .= '/';
			//   print ' < br=""> adding dir ' . $parent_dir . ' < br=""> ';
		}
		$nodes = glob($path . '/*');
		foreach($nodes as $node)
		{
			if(is_dir($node))
			{
				$this->addDir($node, $parent_dir.basename($node));
			}
			else
			if(is_file($node))
			{
				$this->addFile($node, $parent_dir.basename($node));
				//   print 'adding file '.$parent_dir.basename($node) . ' < br=""> ';
			}
		}
	}
} // class Zipper
?>
```

![](https://www.pipiscrew.com/wp-content/uploads/2015/03/snap538.png "snap538")
1-before start the script
2-while user downloading the zip
3-zip downloaded

origin - http://www.pipiscrew.com/?p=2566 phpmysql-export-invoices-each-as-docx-batch-and-download-them-as-zip-file