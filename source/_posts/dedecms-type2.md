---
title: 分享一个dedecms自定义获取上级栏目名称和链接的标签
tags:
  - dedecms
  - php
  - 二次开发
  - 代码
id: '606'
categories:
  - - 笔记
date: 2013-07-08 17:54:56
---

前几天用 **dedecms** 做项目的时候，碰到了一个比较棘手的需求。就是在三级栏目的情况下，要获取它的上级栏目的名字和链接。一开始想着用sql标签来输出，但是因为栏目比较多，可能效率不是很好，于是就弄成了标签的形式。 代码实现如下：

CAttribute->Items,$attlist);
extract($ctag->CAttribute->Items, EXTR\_SKIP);
$innertext = trim($ctag->GetInnerText());

if($typeid==0) {
$typeid = ( isset($refObj->TypeLink->TypeInfos\['topid'\]) ? $refObj->TypeLink->TypeInfos\['topid'\] : $envs\['typeid'\] );
}

//if(empty($typeid)) return '';
if(empty($typeid)) $typeid=$refObj->TypeLink->TypeInfos\['id'\];
//$row=null;
//if()
$row = $dsql->GetOne("Select topid,typedir,isdefault,defaultname,ispart,namerule2,typename,moresite,siteurl,sitepath 
                     From `#@__arctype` where id='$typeid' ");
if(!is\_array($row)) return 'sdfsd';
if(trim($innertext)=='') $innertext = GetSysTemplets("part\_type\_list.htm");

$dtp = new DedeTagParse();
$dtp->SetNameSpace('field','\[','\]');
$dtp->LoadSource($innertext);
if(!is\_array($dtp->CTags))
{
unset($dtp);
return '';
}
else
{
$row\['typelink'\] = GetTypeUrl($row\['topid'\],MfTypedir($row\['typedir'\]),$row\['isdefault'\],
                    $row\['defaultname'\],$row\['ispart'\],$row\['namerule2'\],$row\['siteurl'\],$row\['sitepath'\]);
foreach($dtp->CTags as $tagid=>$ctag)
{
if(isset($row\[$ctag->GetName()\])) $dtp->Assign($tagid,$row\[$ctag->GetName()\]);
}
$revalue = $dtp->GetResult();
unset($dtp);
return $revalue;
}
}
?>

把这个命名为type2.lib.php放在include/taglib目录下面，让后再模板里面调用：

{dede:type2}
    *   [\[field:typename/\]]([field:typelink/])
{/dede:type2}

好记性不如烂笔头，还是记录在此，方便以后查询~