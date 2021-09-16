# Activity Simulations and Codes

## Activity-1 In Action

![image](https://user-images.githubusercontent.com/89735311/133506780-ae55fa0c-68d2-4717-b481-e20fef3a8e54.png)

## Activity Code-1
 
    void peripheral_init(void)
    {	
	 
   
    DDRD |= (1<<PD2); // set PD2=1 for LED
     
    DDRD &= ~(1<<PD0); //clear bit
    PORTD |= (1<<PD0); //set bit PD0 for SeatSwitch
    DDRD &= ~(1<<PD1); //clear bit
    PORTD |= (1<<PD1); //set bit PD0 for HeaterSwitch
    }

    void TurnLED_ON(){
    LED_PORT |= (1<<LED_PIN); 
         }

    void TurnLED_OFF(){
    LED_PORT &= ~(1<<LED_PIN);
     }

    int act1=0;
    int activity1_LED(void)
     {
    
    peripheral_init();
    
    
    if(!(PIND&(1<<BUTTON_SENSOR )) && !(PIND&(1<<TEMP_SENSOR))) //both the switches are pressed
        { 
            act1=1;
        }
       else  //in all other cases
        {
            act1=0;
        }
   
   
      return act1;
      }
  
 ## Activity-2 In Action

![image](https://user-images.githubusercontent.com/89735311/133507852-6c9c2ea6-d8a8-4188-99c2-75de978f196c.png)

## Activity Code-2

     void InitADC()
    {
    
    ADMUX=(1<<REFS0);
    ADCSRA= (1<<ADEN)|(7<<ADPS0);
    }

    uint16_t ReadADC(uint8_t ch)
    {
    
    ADMUX&=0xf8;
    ch=ch&0b00000111;
    ADMUX|=ch;

    ADCSRA|=(1<<ADSC);
    while(!(ADCSRA & (1<<ADIF)));
    ADCSRA|=(1<<ADIF);
    return(ADC);
     }

    uint16_t activity2_GetADC(void)
    {
       
       InitADC();
      uint16_t temp;
      temp=ReadADC(0);
      return temp;
      }
      
##  Activity-3 In Action

![image](https://user-images.githubusercontent.com/89735311/133508326-25fd4003-7b20-40e3-84c0-fb69b5251a6d.png)

![image](https://user-images.githubusercontent.com/89735311/133508365-1e064219-da87-4e81-9bcf-bd79dd393df7.png)

## Activity Code-3

     void InitTimer()
     {
    TCCR1A |= (1<<COM1A1)|(1<<WGM11)|(1<<WGM10);
    TCCR1B |= (1<<WGM12)|(1<<CS11)|(1<<CS10);
    DDRB |=(1<<PB1);
    }

    void activity3_PWM(uint16_t temp)
    {
    InitTimer();
    if(temp>=0 && temp<=200){
            OCR1A = PWM_20_PERCENT;
            _delay_ms(200);
        }
        else if(temp>=210 && temp<=500){
             OCR1A = PWM_40_PERCENT;
            _delay_ms(200);
        }
        else if(temp>=510 && temp<=700){
             OCR1A = PWM_70_PERCENT;
            _delay_ms(200);
        }
        else if(temp>=710 && temp<=1024){
             OCR1A = PWM_95_PERCENT;
            _delay_ms(200);
        }
        else{
            OCR1A=0;
            _delay_ms(200);
        }

       }



  
