# java-web-project
package com.lh.bean;

public class StringUtil {
	private String money;		
	private String submoneyCN[]={"","拾","佰","仟"};									//表示数字位数的数组
	private String numberCNN[]={"零","壹","贰","叁","肆","伍","陆","柒","捌","玖"};	
	private String je="零壹贰叁肆伍陆柒捌玖";		
	private String cdw="万仟佰拾亿仟佰拾万仟佰拾元角分";	
	public StringUtil(){}		
	public void setMoney(String money){
		this.money=money;
	}
	public String getMoney(){
		return convert(this.money);
		
	}
	public String convert(String money){
	  String formatCN="";	
	  int point=money.indexOf(".");				
      if(point!=-1){
	    String money1=money.substring(0,point);	
	    String money1_1=(new StringBuffer(money1).reverse()).toString();
	    String money2=money.substring(point+1);	
	    if(money2.length()<2){				
	    	if(money2.length()==0)
	    		money2="00";
	    	else
	    		money2+="0";
	    }
	    else								
	    	money2=money.substring(point+1,point+3);
	    int len = money1_1.length();		
	    int pos=len-1;
	    String sigle="";
	    boolean allhavenum=false;
	    boolean havenum=false;
	    boolean mark=false;       				
	    while(pos>=0){
		    sigle=money1_1.substring(pos,pos+1);    
		    if(pos>=8&&pos<12){ 
			    if(!sigle.equals("0")){      	
				    if(!mark){               	 
				    	formatCN+=numberCNN[Integer.parseInt(sigle)]+submoneyCN[pos%4];
				    }
				    else{                    	     	
if(allhavenum){        
				    		formatCN+="零";
				    	}
				    	formatCN+=numberCNN[Integer.parseInt(sigle)]+submoneyCN[pos%4];
				        mark=false;
				    }
				    havenum=true;
				    allhavenum=true;        				    }
			    else{                      		
				    mark=true;


			    }
			    if(pos%4==0&&havenum){     
			    	formatCN+="亿";
		    	    havenum=false;
			    }
		    }
	    
		    if(pos>=4&&pos<8){
    			if(!sigle.equals("0")){
				    if(!mark)
				    	formatCN+=numberCNN[Integer.parseInt(sigle)]+submoneyCN[pos%4];
	    			else{
	    				if(allhavenum){
	    					formatCN+="零";
	    				}
	    				formatCN+=numberCNN[Integer.parseInt(sigle)]+submoneyCN[pos%4];
			    		mark=false;
				    }
				    havenum=true;
				    allhavenum=true;
			    }
			    else{
    			    mark=true;
	    		}
		    	if(pos%4==0&&havenum){ 
		    		formatCN+="万";
				    havenum=false;
			    }
		    }
	
		    if(pos>=0&&pos<4){
    			if(!sigle.equals("0")){        
    				if(!mark)
    					formatCN+=numberCNN[Integer.parseInt(sigle)]+submoneyCN[pos%4];
				    else{ 
				    	if(allhavenum){
				    		formatCN+="零";
				    	}
				    	formatCN+=numberCNN[Integer.parseInt(sigle)]+submoneyCN[pos%4];
					    mark=false;       
				    }
    				havenum=true;
    				allhavenum=true;
			    }
			    else{
    				mark=true;
	    		}
		    }
		    pos--;    		
	    }
	 
        if(allhavenum)           	formatCN+="元";
        else           
        	formatCN="零元";
           
        if(money2.equals("00"))
        	formatCN+="整";
        else{
        	if(money2.startsWith("0")||(allhavenum&&money1.endsWith("0"))){ 
        		formatCN+="零";
	        }
        	if(!money2.startsWith("0")){
        		formatCN+=numberCNN[Integer.parseInt(money2.substring(0,1))]+"角";
	        }
        	
        	formatCN+=numberCNN[Integer.parseInt(money2.substring(1))]+"分";
        }
      } 
      else{
    	  formatCN="输入的格式不正确！格式：888.00";
      }
      return formatCN;
    }
}


