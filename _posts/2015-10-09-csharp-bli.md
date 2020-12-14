---
title: o[csharp] blinking rainbow label
author: PipisCrew
date: 2015-10-09
categories: [.net]
toc: true
---

reference 
http://rainbow.arch.scriptmania.com/tools/rainbow_text/

```js
        public Form1()
        {
            InitializeComponent();

            this.Text = Application.ProductName + " v" + Application.ProductVersion;

            timer1.Interval = 30;
        }

        string[] colors = new string[] { "#FF0000", "#FF2100", "#FF4200", "#FF6300", "#FF8400", "#FFA500", "#FFC600", "#FFE700", "#FFff00", "#DEff00", "#BDff00", "#9Cff00", "#7Bff00", "#5Aff00", "#39ff00", "#18ff00", "#00ff00", "#00ff21", "#00ff42", "#00ff63", "#00ff84", "#00ffA5", "#00ffC6", "#00ffE7", "#00ffff", "#00E7ff", "#00C6ff", "#00A5ff", "#0084ff", "#0063ff", "#0042ff", "#0021ff", "#0000ff", "#1800ff", "#3900ff", "#5A00ff", "#7B00ff", "#9C00ff", "#BD00ff", "#DE00ff", "#FF00ff", "#FF00E7", "#FF00C6", "#FF00A5", "#FF0084", "#FF0063", "#FF0042" };
        int color_current = 0;

        private void timer1_Tick(object sender, EventArgs e)
        {
            if (color_current > colors.Length - 1)
                color_current = 0;

            label3.ForeColor = System.Drawing.ColorTranslator.FromHtml(colors[color_current]);

            color_current += 1;
        }
```

* * *

##  HTML Rainbow Generator

```js
//source - http://www.draac.com/rainbow.html
<?php *="" title="" and="" meta="" tag="" variables="" */="" $title='Draac.Com Rainbow Text Maker' ;="" $meta_keywords='free,secret,html,css,tables,frames,help,webtv,draac,drac,dracc,draak,drake,gifs123,gifs,animation,animate,web,design,building,build,internet,webmaster,computer,software,download,downloads,driver,drivers,font,fonts,code,codes,meta,resource,images,sounds,promotion,promote,jokes,laughs,freeemail,draacmail,email,link,links,site,page,effect,text,tips,tricks,webmasters,scrolling,games,jokes,funny,kiss,virtual,layout,puzzle,puzzles,help,webmasters,home,page' ;="" $meta_description='Visit this site for the best FREE html, table & frames courses on the internet! Get a FREE DraacMail Account to email your friends from anywhere in the world !' ;=""?>

<!--

/*
	name   : nt.js (not in a separate file)
	date   : 2000-02-26 (a few cosmetic enhancements, nothing majorly new)
	author : A. Gunther
	www    : http://home.earthlink.net/~redbird77
	email  : redbird77@earthlink.net

	Use this script however you want.  Improve upon it, slice it, dice it,
	whatever..., but try to leave the comments and credits intact.
*/

function makePreview(f)
{
	var s = '';

	s += '<title>Preview<\/title><\/head>'
	s += '<center><p>**Here is what your text will look like.<\/b><\/center>

* * *
' + f.results.value
	s += '

* * *
<p>**Webtv Users Scroll Up Back To The Generator.**  

<center><form><input class="buttn" type=button value=\"Close Window\" onClick=\"self.close()\"><\/form><\/center>'
	s += '<\/p><\/body><\/html>'

	var w = window.open('', 'winPreview', 'resizable=yes,width=500,height=300,screenX=0,screenY=0')
	w.document.write(s)
	w.document.close()
}

var c = '0123456789ABCDEF';
function HEXtoDEC(n){n=n.toUpperCase();return c.indexOf(n.charAt(0))*16+c.indexOf(n.charAt(1))}
function DECtoHEX(n){return c.charAt((n>>4)&0xF)+c.charAt(n&0xF)}

function toAlt(f)
{
	var ALPHA     = 'abcdefghijklnopqrstuvxyz';
	var ALT_ALPHA = 'ÃßÇÐèƒgHïJK£Ñõpq®Š†ÚV×ÝZ';
	var txt       = (f.txtUser.value).toLowerCase();
	var pos, i;

	f.txtUser.value = '';

	for (i = 0, ltr = txt.charAt(i); i < txt.length; ltr = txt.charAt(++i))
	{
		if (ltr == 'm') ltr = '\/\\/\\';
		else if (ltr == 'w') ltr = '\\/\\/';
		else
		{
			pos = 0;
			while (ltr != ALPHA.charAt(pos) && pos < ALPHA.length) pos++;
			ltr = ALT_ALPHA.charAt(pos);
		}

		f.txtUser.value += (pos == ALPHA.length ? txt.charAt(i) : ltr);
	}
}

function getRandomColor()
{
	var i, col;
	for (col = '', i = 0; i < 3; i++) col += DECtoHEX(Math.floor(Math.random() * 256));
	return col;	
}

function toRandom(str)
{
	var i    = 0
	var sRet = '';

	while (i < str.length) sRet += str.charAt(i++).fontcolor(getRandomColor());

	return sRet;
}

function makeHTML(f)
{
	var waveit  = '';
	var add_tag = true;

	var max  = 0;
	var num  = 0;
	var numw = 1;
	var inc  = 1;
	var incw = 1;

	var hex_r, hex_g;

	var output = '';
	var s_tag = '';
	var ltr;

	var pG = new Array('00','11','22','33','44','55','66','77','88','99','aa','bb','cc','dd','ee','ff');

	var colors = new Array(30);
	colors[0]='ff00ff';colors[1]='ff00cc';colors[2]='ff0099';colors[3]='ff0066';
	colors[4]='ff0033';colors[5]='ff0000';colors[6]='ff3300';colors[7]='ff6600';
	colors[8]='ff9900';colors[9]='ffcc00';colors[10]='ffff00';colors[11]='ccff00';
	colors[12]='99ff00';colors[13]='66ff00';colors[14]='33ff00';colors[15]='00ff00';
	colors[16]='00ff33';colors[17]='00ff66';colors[18]='00ff99';colors[19]='00ffcc';
	colors[20]='00ffff';colors[21]='00ccff';colors[22]='0099ff';colors[23]='0066ff';
	colors[24]='0033ff';colors[25]='0000ff';colors[26]='3300ff';colors[27]='6600ff';
	colors[28]='9900ff';colors[29]='cc00ff';

	var wX = new Array('ff0000','ff3333','ff6666','ff9999','ffcccc','ffffff','ccffcc','99ff99','66ff66','33ff33','00ff00', '33ff33','66ff66','99ff99', 'ccffcc','ffffff','ffcccc','ff9999','ff6666','ff3333');

	var bX = new Array('ff0000','cc0000','990000','660000','330000','000000','003300','006600','009900','00cc00','00ff00','00cc00', '009900','006600','003300','000000','330000','660000','990000','cc0000');

	if (f.rad[0].checked && (!f.optDesign[1].checked)) add_tag = false;

	for (var i = 0; i < (f.txtUser.value).length; i++)
	{
		hex_r = DECtoHEX(Math.floor(Math.random() * 256));
		hex_g = DECtoHEX(Math.floor(Math.random() * 256));

		if (f.optDesign[1].checked) waveit = ' size=' + numw;

		if (f.rad[0].checked) s_tag = waveit != '' ?  '<font' + waveit + '>' : '';
		else if (f.rad[1].checked){s_tag = '<font color=' + colors[num] + waveit + '>';max = 29}
		else if (f.rad[2].checked){s_tag = '<font color=' + 'ff' + pG[num] + '00' + waveit + '>';max = 15}
		else if (f.rad[3].checked) s_tag = '<font color=' + getRandomColor() + waveit + '>';
		else if (f.rad[4].checked) s_tag = '<font color=' + hex_r + '0000 size=' + Math.ceil(Math.random() * 7) + '>';
		else if (f.rad[5].checked) s_tag = '<font color=' + hex_r + hex_g + '00' + waveit + '>';
		else if (f.rad[6].checked){s_tag = '<font color=' + wX[num] + waveit + '>';max = 19}
		else{s_tag = '<font color=' + bX[num] + waveit + '>';max = 19}

		ltr = f.txtUser.value.charAt(i);

		if (ltr != ' ')
		{
			if (f.optDesign[2].checked && (i & 1)) ltr = ltr.toUpperCase();
			output = add_tag ? (s_tag + ltr + '<\/font>') : ltr;
			num += inc;
			numw += incw;
			if (numw == 7 || numw == 1) incw *= -1;
			if (num == max || !num) inc *= -1;
		}
		else
			output = f.chkPic.checked ? ('<img src="' + f.txtUserPic.value + '">') : ltr;

		f.results.value += output;
	}
}
//-->

<div class="body_container">
	<div class="bg_body_bubble"> </div>

	<?php include('navigation.php');=""?>

	<div class="flt_left" id="right_panel">
		<div>![](images/trans.gif)</div>

			<div class="inner_page_content">

						<div>
							<div class="inner_box" id="top">
								<div>
									<div class="flt_left">

# <span>Create Some Rainbow Text</span>

</div>
									<div class="flt_left gray_rounded"> </div>
									<div class="clr"></div>
								</div>

							  <div class="inner_box_body inner_cont_padd">

								<!-- 22-04-11 -->
									<div class="inner_box_cont" id="box">
										<div class="tab_format_container tab_border">
											<div>

											<form action="">

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**1<sup>st</sup> Enter your text here:**</font>

<table cellpadding="5" cellspacing="0" width="100%">
	<tbody><tr align="left"><td><input name="txtUser" size="65" type="text"></td></tr>

</tbody></table>

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**2<sup>nd</sup> Choose a color scheme:**</font>

<table border="1" style="padding:2px;" bordercolor="#8aa800" cellpadding="5" cellspacing="1" width="500">
	<tbody><tr bgcolor="#ffffff">
<td width="50%"><input style="" name="rad" checked="checked" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Plain**</font></td>
		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Rainbow**</font></td>
	</tr>
	<tr bgcolor="#ffffff">
		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Flame**</font></td>
		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Random**</font></td>

	</tr>
	<tr bgcolor="#ffffff">
		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Scary**</font></td>
		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Autumn**</font></td>
	</tr>
	<tr bgcolor="#ffffff">
		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Christmas (light)**</font></td>

		<td width="50%"><input style="" name="rad" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Christmas (dark)**</font></td>
	</tr>
</tbody></table>

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**3<sup>rd</sup> Choose a text design:**</font>

<table border="1" style="padding:2px;" bordercolor="#8aa800" cellpadding="5" cellspacing="1" width="500">
	<tbody><tr align="left" bgcolor="#ffffff">
		<td width="33%"><input style="" name="optDesign" checked="checked" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Straight**</font></td>

		<td width="33%"><input style="" name="optDesign" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Wavy**</font></td>
		<td width="34%"><input style="" name="optDesign" type="radio"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Alternating Case**</font></td>
	</tr>
</tbody></table>

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**4<sup>th</sup> Use an image in place of the spaces between words:**</font>

<table border="1" style="padding:2px;" bordercolor="#8aa800" cellpadding="5" cellspacing="1" width="500">
	<tbody><tr align="center" bgcolor="#ffffff">

		<td align="center"><input name="chkPic" type="checkbox"><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Yes**</font></td>

		<td style="padding:15px 0 0 0;">[<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**URL**</font>](javascript:void(0)) <font color="#0000cd" face="verdana,arial,helvetica,sans-serif" size="2">**:**</font> <input name="txtUserPic" size="35" type="text">

 <font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Note: This feature is optional**</font>
</td>
	</tr>	
</tbody></table>

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif " size="2">**5<sup>th</sup> Make the HTML or clear the form:**</font>

<table border="1" style="padding:2px;" bordercolor="#8aa800" cellpadding="5" cellspacing="1" width="500">
	<tbody><tr align="center" bgcolor="#ffffff">
		<td width="50%"><input class="buttn" value="Make HTML Code" onclick="makeHTML(this.form)" type="button">

<font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**CLICK ONCE - Code is below**</font>
</td>
		<td width="50%" style="padding:15px 0 0 0;"><input class="buttn" value="Clear" type="reset">

<font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Clear the whole form**</font>
</td>
	</tr>
</tbody></table>

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**6<sup>th</sup> Preview your results - Select a background color:**</font>

<table border="1" style="padding:2px;" bordercolor="#8aa800" cellpadding="5" cellspacing="1" width="500">
	<tbody><tr align="center" bgcolor="#ffffff">
		<td><input class="buttn" value="Preview" onclick="makePreview(this.form)" type="button"></td>
		<td><font color="#48494A" face="verdana,arial,helvetica,sans-serif" size="2">**Background**</font> [<font color="#8aa800" face="verdana,arial,helvetica,sans-serif" size="2">**color**</font>](javascript:void(0))<font color="#0000cd" face="verdana,arial,helvetica,sans-serif" size="2"> **:**</font> <input name="txtPreCol" size="10" value="white" type="text">
</td>
	</tr>
</tbody></table>

<font color="#8aa800" face="verdana,arial,helvetica,sans-serif">**7<sup>th</sup> Here is your HTML code:**</font>

 <textarea name="results" cols="60" rows="20" style="width:500px; margin:0 0 0 0px;"></textarea>

</form>

</div>

**Script Used With Permission, Script By A. Gunther  
 [http://home.earthlink.net/~redbird77](http://home.earthlink.net/%7Eredbird77)**

										</div>

									  <div class="inner_list_boxextra ul_toppad">

									  </div>

                              </div>
							</div>

							<div class="pagination">
								[Home](index.html)  

							</div>

					  </div>

<div>![](images/trans.gif)</div>
				  </div>

				  </div>

	</div>

</div>

<?php include('footer.php');=""?>
```

origin - http://www.pipiscrew.com/?p=2126 csharp-blinking-rainbow-label