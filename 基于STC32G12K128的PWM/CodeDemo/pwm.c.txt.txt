#include "pwm.h"

uint16 duty[4]={0,0,0,0},hz[4]={0,0,0,0};
extern uint8 pwm_choose,pwm_set_flag,key_push_a_time_flag,key_push_c_time_flag;
extern int32 key_push;

void pwm_start(void)
{
	if(key_push_a_time_flag)key_push-=10;
	if(key_push_c_time_flag)key_push+=10;
	key_push_a_time_flag=0;
	key_push_c_time_flag=0;
	if(pwm_set_flag==1)
	{
		//key_rotate=hz[pwm_choose-1];
		if(key_push>=3000000)key_push=3000000;
		if(key_push<=1)key_push=1;
		hz[pwm_choose-1]=key_push*10;
	}
	if(pwm_set_flag==2)
	{
		//key_rotate=duty[pwm_choose-1];
		if(key_push>=100)key_push=100;
		if(key_push<=0)key_push=0;
		duty[pwm_choose-1]=key_push;
	}
	switch(pwm_choose)//duty_set
	{
		case 1:{pwm_freq(PWMA_CH3P_P24,hz[0],duty[0]*100);}break;
		case 2:{pwm_freq(PWMB_CH2_P21 ,hz[1],duty[1]*100);}break;
		case 3:{pwm_freq(PWMB_CH1_P20 ,hz[2],duty[2]*100);}break;
		case 4:{pwm_freq(PWMA_CH4P_P34,hz[3],duty[3]*100);}break;
		default:break;
	}
//		pwm_duty(PWMA_CH1P_P10,duty[0]*100);
//		pwm_duty(PWMA_CH4P_P16,duty[1]*100);
//		pwm_duty(PWMB_CH1_P17 ,duty[2]*100);
//		pwm_duty(PWMB_CH3_P33 ,duty[3]*100);
//	pwm_freq(PWMA_CH1P_P10,hz[0],duty[0]*100);
//	pwm_freq(PWMA_CH4P_P16,hz[1],duty[1]*100);
//	pwm_freq(PWMB_CH1_P17 ,hz[2],duty[2]*100);
//	pwm_freq(PWMB_CH3_P33 ,hz[3],duty[3]*100);
	delay_ms(100);
}
