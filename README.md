# Vaja7-PWM-NUCLEO

PINOUT slika:\
![pinout](https://github.com/Hudi452/Vaja7-PWM-NUCLEO/blob/main/MX%20pinout.png)


IZREZEK konfiguracijskega okna (TIM1,  Parameter Settings):\
![konfig](https://github.com/Hudi452/Vaja7-PWM-NUCLEO/blob/main/Timer_configuration.png)


FOTOGRAFIJA vezja:\
![vezje](https://github.com/Hudi452/Vaja7-PWM-NUCLEO/blob/main/Slika_vezja.png)


FOTOGRAFIJA osciloskopa:\
![osciloskop](https://github.com/Hudi452/Vaja7-PWM-NUCLEO/blob/main/Slika_osciloskopa.png)



VIDEO POSNETKI delovanja:

1. Duty Cycle = 50%:
   

2. DutyCycle = 25%:
   

3. Duty Cycle se spreminja:

   


ODGOVORI NA VPRAŠANJA:\
2.)\
b)Omogočili smo pin PA8. Poleg pina se izpiše TIM1_CH1.\
d)Vrednost Prescaler je 16.\
e) Po tem ko Counter Period nastavimo na 100 znaša takt časovnika 10 kHz.\
f) Pod PWM Generation Channel Pulse nastavimo vrednost delovnega cikla (Duty Cycle). Delovni cikel je razmerje med trajanjem impulza in periodo PWM signala.
S tem ko pod PWM Generation Channel Pulse zapišemo vrednost 50, dosežemo 50% delovni cikel.\
3.)\
b) Ukaz za Pulse, ki ga je generiral CubeMX: sConfigOC.Pulse = 50;\
c) Inicializacija časovnika za PWM signal:\
HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_1);\
4.)\
f)Čas ene periode T = 26,84 µs in čas aktivnega impulza Ton = 13,42 µs iz osciloskopa.\
5.)\
a) Ukaz za spremembo širine impulza na 25%: sConfigOC.Pulse = 25;\
g) Razlaga naslednjih ukazov:\
htim1.Instance->CCR1 = dutyCycle;\
dutyCycle+=10;\
if(dutyCycle>90) dutyCycle=10;\
HAL_Delay(1000);

Z ukazom htim1.Instance->CCR1 = dutyCycle; vstavimo v register CCR1, ki je odgovoren za širino impulza našega PWM signala, vrednost spremenljivke dutyCycle.\
Z ukazom dutyCycle+=10; povečamo vrednost spremenljivke dutyCycle za 10.\
Z ukazom if(dutyCycle>90) dutyCycle=10; zapišemo spremenljivki dutyCycle vrednost 10, če je ta večja od 90.\
Z ukazom HAL_Delay(1000); počakamo eno sekundo.

KOMENTAR:\
Z osciloskopom smo izmerili PWM signale, ki jih generira STM32. Najprej smo z osciloskopom izmerili PWM signal z delovnim ciklom 50% (impulz traja polovico periode), nato pa smo program spremenili tako, da smo lahko generirali PWM signal z delovnim ciklom 25% (impulz traja četrtino periode). Na koncu pa smo STM32 sprogramirali tako, da se širina impulza PWM signala postopoma povečuje od 10% do 90% periode. Za tem pade širina impulza ponovno na 10% periode in postopek se ponovi.



