---
layout: post
title: "Thinkphp&dwz三级联动下拉菜单"
tags:
- Thinkphp
- dwz

---

Tpl\ComBox\index.html：

	<h2 class="contentTitle">下拉菜单</h2>  
  
	<div class="pageContent" layoutH="56">  
    	<select class="combox" name="province" ref="w_combox_city" refUrl="__URL__/returnCity/cityId/{value}">  
        	<option value="all">所有省市</option>  
        	<option value="bj">北京</option>  
        	<option value="sh">上海</option>  
    	</select>  
    	<select class="combox" name="city" id="w_combox_city" ref="w_combox_area" refUrl="__URL__/returnArea/areaId/{value}">  
        	<option value="all">所有城市</option>  
    	</select>  
    	<select class="combox" name="area" id="w_combox_area">  
        	<option value="all">所有区县</option>  
    	</select>  
	</div> 

Action\ComBoxAction.class.php：

    <?php  
    // 三级联动下拉菜单  
    class ComBoxAction extends CommonAction {      
           
        public function returnCity(){  
            $cityId = $_REQUEST['cityId'];  
            if($cityId=='sh'){  
                $arrCity = array(array('all','所有城市'),array('sh','上海市'));  
            }else if($cityId=='bj'){  
                $arrCity = array(array('all','所有城市'),array('bj','北京市'));  
            }else{  
                $arrCity = array(array('all','所有城市'));  
            }  
             echo json_encode($arrCity);  
        }  
          
        public function returnArea(){  
            $areaId = $_REQUEST['areaId'];  
            if($areaId=='sh'){  
                $arrArea = array(array('1','上海城市1'),array('2','上海城市2'));  
            }else if($areaId=='bj'){  
                $arrArea = array(array('3','北京城市3'),array('bj','北京城市4'));  
            }else{  
                $arrArea = array(array('all','所有城市'));  
            }  
              
             echo json_encode($arrArea);  
        }  
          
    }  