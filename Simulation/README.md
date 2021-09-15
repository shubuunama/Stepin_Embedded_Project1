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
  
