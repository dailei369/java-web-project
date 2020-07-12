# java-web-project
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
