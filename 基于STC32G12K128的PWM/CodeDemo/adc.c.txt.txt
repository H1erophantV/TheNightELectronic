#include "adc.h"

uint16 ad1_result,ad2_result;
uint32 temp1,temp2;
double adc1=0,adc2=0;

void adc_detection(void)
{
	
	ad1_result = adc_once(ADC_P01, ADC_12BIT);
	temp1 = (((uint32)ad1_result * 5070) / 4096);  //¼ÆËã³öµ±Ç°adcÒý½ÅµÄµçÑ¹ ¼ÆËã¹«Ê½Îª ad_result*VCC/ADC·Ö±æÂÊ    VCCµ¥Î»Îªmv
	adc1 =  (double)temp1 * 11/1000;//¸ù¾ÝÒý½ÅµçÑ¹  ºÍ·ÖÑ¹µç×èµÄ×èÖµ¼ÆËãµç³ØµçÑ¹ ¼ÆËã¹«Ë¾Îª   Òý½ÅµçÑ¹*(R2+R3)/R3   R3Îª½ÓµØ¶Ëµç×è

	ad2_result = adc_once(ADC_P00, ADC_12BIT);
	temp2 = (((uint32)ad2_result * 5070) / 4096);  //¼ÆËã³öµ±Ç°adcÒý½ÅµÄµçÑ¹ ¼ÆËã¹«Ê½Îª ad_result*VCC/ADC·Ö±æÂÊ    VCCµ¥Î»Îªmv
	adc2 =  (double)temp2 * 11/1000;//¸ù¾ÝÒý½ÅµçÑ¹  ºÍ·ÖÑ¹µç×èµÄ×èÖµ¼ÆËãµç³ØµçÑ¹ ¼ÆËã¹«Ë¾Îª   Òý½ÅµçÑ¹*(R2+R3)/R3   R3Îª½ÓµØ¶Ëµç×è
	
	delay_ms(100);
}
