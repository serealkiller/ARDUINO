#include <LedControl.h>

LedControl syahwil = LedControl(7,6,5,1);

int tombol_start_stop = 2;
int tombol_reset = 3;
int count_ms = 0;
int count_detik = 0;
int count_menit = 0;
int count_jam = 0;

long lastTime, millisTime, deltaTime = 0;

const int led_jam = 11;
const int led_menit = 12;

int status_tombol_start_stop_sblm = LOW;
int status_tombol_reset_sblm = LOW;
int sedang_dipause = HIGH;


void setup()
 { 
 
 syahwil.shutdown (0,false);
 syahwil.setIntensity (0,15);
 syahwil.clearDisplay (0);
 pinMode (tombol_start_stop, INPUT);
 pinMode (tombol_reset, INPUT);
 pinMode (led_menit, OUTPUT);
 pinMode (led_jam, OUTPUT);
 digitalWrite (led_menit, HIGH);
 digitalWrite (led_jam, HIGH);
 
 }

 
void loop()

 { 
 cek_saklar();
 kontrol_timer();
 
 }
 
 void kontrol_timer ()
 {
 if (sedang_dipause)return;
 
 millisTime = millis();
   deltaTime = millisTime-lastTime;
 if ( deltaTime>10 )
 {
   count_ms++;
   lastTime = millisTime;
 }
 
 tampilkan_waktu();
 
 }


void tampilkan_waktu ()

{

int digit_satuan_ms = count_ms %10;
int digit_puluhan_ms = (count_ms/10);
int digit_satuan_detik =count_detik%10;
int digit_puluhan_detik =(count_detik/10);
int digit_satuan_menit =count_menit%10;
int digit_puluhan_menit =(count_menit/10);
int digit_satuan_jam =count_jam %10;
int digit_puluhan_jam =(count_jam/10);

if(count_ms >= 100) {
count_detik++;
count_ms =0;
}
 if (count_detik >59) {
 count_menit++;
 count_detik =0;
 }
  if (count_menit > 59) {
  count_jam++;
  count_menit =0;
  }
  if (count_jam >=24){
  sedang_dipause = !sedang_dipause;
  count_ms=0;
  count_detik=0;
  count_menit=0;
  count_jam=24;
  }
syahwil.setDigit (0,0,byte(digit_satuan_ms),false);
syahwil.setDigit (0,1,byte(digit_puluhan_ms),false);
syahwil.setDigit (0,2,byte(digit_satuan_detik),true);
syahwil.setDigit (0,3,byte(digit_puluhan_detik),false);
syahwil.setDigit (0,4,byte(digit_satuan_menit),false);
syahwil.setDigit (0,5,byte(digit_puluhan_menit),false);
syahwil.setDigit (0,6,byte(digit_satuan_jam),false);
syahwil.setDigit (0,7,byte(digit_puluhan_jam),false);

} 


void cek_saklar(){
int val_tombol_start_stop = digitalRead(tombol_start_stop);
   int val_tombol_reset = digitalRead(tombol_reset);
   
   if (val_tombol_reset == LOW && status_tombol_reset_sblm==HIGH)
   {
      count_jam=0;
      count_menit=0;
      count_detik=0;
      count_ms=0;
      sedang_dipause = HIGH;
      delay(200);
      }
      status_tombol_reset_sblm=val_tombol_reset;
      
      if (val_tombol_start_stop == LOW && status_tombol_start_stop_sblm==HIGH){
      sedang_dipause=!sedang_dipause;
      delay(200);
      }
      status_tombol_start_stop_sblm=val_tombol_start_stop;
      tampilkan_waktu();
}
