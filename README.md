# Krakatoid
Denys Plaud <denys.plaud1@gmail.com>
Krakatoid
Denys Plaud <denys.plaud1@gmail.com> 7 avril 2019 à 16:20
À : Denys Plaud <denys.plaud1@gmail.com>
package com.denysplaud.krakatoid;

// Krakatoid s'est envolé samedi 6 avril 2019...
// Bon amusement!Pour toute question->denys.plaud1@gmail.com

import android.hardware.*;
import android.os.*;
import android.app.*;
import android.widget.*;
import android.content.*;
import android.view.*;
import java.util.*;
import android.content.pm.*;
import android.media.*;
import android.graphics.*;
import android.text.*;
import android.text.style.*;
import android.speech.tts.TextToSpeech;
import android.speech.tts.TextToSpeech.OnInitListener;
import android.speech.tts.*;

class Tdvals{
private long t;
private float[] f;

public Tdvals(){ 
t=0;
f=new float[]{0,0,0};
}
public void setT(long t){
this.t=t;
}
public void setF(float[]f){
this.f=f;
}
public long getT(){
return t;
}
public float[] getF(){
return f;
}
}
class Jakapie extends View{
private int hauteur;
private int largeur;
private int numpie;
private float xpie;
private float ypie;
private int anglepie;
private String mot;
public Jakapie(Context context){
super(context);
}
public void setpie(int hauteur,int largeur,int numpie,float xpie,float ypie,int anglepie,String mot){
this.hauteur=hauteur;
this.largeur=largeur;
this.numpie=numpie;
this.xpie=xpie; 
this.ypie=ypie;
this.anglepie=anglepie;
this.mot=mot;
}
@Override
protected void onDraw(Canvas canvas)
{ 
super.onDraw(canvas);
Paint paint=new Paint();
// paint.setTextSize(30); 
if(numpie==1){ 
// transformations de vol
// préciser l'angle de la rotation,en degrés,et son centre 
canvas.rotate(anglepie,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// applique symétrie d'axe vertical par rapport au repére tourné, si recul,obtenu qd anglepie<0,voir coordopie()
if(anglepie<0)canvas.scale(-1,1,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
float uni=540/14;
canvas.scale(0.5f,0.5f,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// ailespie 
paint.setStrokeWidth(9);
float longueurpie=11*uni;
canvas.drawRect((float)(xpie*largeur*10)/20-7*uni,(float)(ypie*hauteur*10)/20-uni/4,(float)(xpie*largeur*10)/20-7*uni+longueurpie,(float)(ypie*hauteur*10)/20+uni/4,paint);
float ailepie=3*uni; 
float anglaile=(float)Math.toDegrees(Math.atan2(uni,ailepie));
for(int i=0;i<2;i++){
canvas.scale(1,(float)Math.pow(-1,i),(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
canvas.rotate(anglaile,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
canvas.drawRect((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20-ailepie,(float)(xpie*largeur*10)/20+4*uni,(float)(ypie*hauteur*10)/20-2*ailepie/3,paint);
canvas.drawRect((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20-ailepie/3,(float)(xpie*largeur*10)/20+4*uni,(float)(ypie*hauteur*10)/20,paint); 
canvas.rotate(-anglaile,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
} 
for(int i=0;i<2;i++){
canvas.scale(1,(float)Math.pow(-1,i),(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
canvas.rotate(anglaile,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
paint.setColor(Color.rgb(240,240,240));
canvas.drawRect((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20-2*ailepie/3,(float)(xpie*largeur*10)/20+4*uni,(float)(ypie*hauteur*10)/20-ailepie/3,paint); 
canvas.rotate(-anglaile,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
}
paint.setColor(Color.BLACK); 
float queuepie=1f*uni;
paint.setStrokeWidth(13);
for(int i=0;i<2;i++){ 
canvas.scale(1,(float)Math.pow(-1,i),(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
canvas.rotate(anglaile,(float)(xpie*largeur*10)/20-7*uni,(float)(ypie*hauteur*10)/20); 
canvas.drawLine((float)(xpie*largeur*10)/20-7*uni,(float)(ypie*hauteur*10)/20-queuepie,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20-queuepie-uni,paint); 
canvas.rotate(-anglaile,(float)(xpie*largeur*10)/20-7*uni,(float)(ypie*hauteur*10)/20); 
} 
canvas.scale(1,-1,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// tête 
paint.setStrokeWidth(9);
float tetepie=uni; 
paint.setColor(Color.GREEN);
canvas.drawCircle((float)(xpie*largeur*10)/20+5*uni,(float)(ypie*hauteur*10)/20,uni,paint);
// antennes 
paint.setColor(Color.rgb(0,155,0));
paint.setStrokeWidth(5);
canvas.drawLine((float)(xpie*largeur*10)/20+5*uni-uni/2,(float)(ypie*hauteur*10)/20-uni/2,(float)(xpie*largeur*10)/20+5*uni-uni/2-uni/4,(float)(ypie*hauteur*10)/20-3*uni/2,paint);
canvas.drawLine((float)(xpie*largeur*10)/20+5*uni+3*uni/4,(float)(ypie*hauteur*10)/20-uni/2,(float)(xpie*largeur*10)/20+6*uni,(float)(ypie*hauteur*10)/20-3*uni/2,paint);
paint.setColor(Color.rgb(240,240,240));
canvas.drawRect((float)(xpie*largeur*10)/20+4*uni,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+6*uni,(float)(ypie*hauteur*10)/20+uni,paint); 
// yeux 
paint.setStrokeWidth(7);
canvas.drawPoint((float)(xpie*largeur*10)/20+5*uni,(float)(ypie*hauteur*10)/20-uni/2,paint);
canvas.drawPoint((float)(xpie*largeur*10)/20+5*uni+uni/2,(float)(ypie*hauteur*10)/20-uni/2,paint); 
paint.setColor(Color.BLACK);
// bec 
paint.setStrokeWidth(3); 
for(int i=0;i<11;i++)canvas.drawLine((float)(xpie*largeur*10)/20+5*uni+i*uni/10,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+7*uni,(float)(ypie*hauteur*10)/20+uni,paint); 
canvas.drawPoint((float)(xpie*largeur*10)/20+largeur/2,(float)(ypie*hauteur*10)/20-5*hauteur/2,paint);
canvas.scale(2f,2f,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// transformations de vol inverses de celles du début,pour retrouver le canevas initial
if(anglepie<0)canvas.scale(-1,1,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
canvas.rotate(-anglepie,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// repére
/* paint.setColor(Color.BLUE); 
paint.setStrokeWidth(7);
for(int i=-7;i<=7;i++)canvas.drawPoint((float)(xpie*largeur*10)/20+i*uni,(float)(ypie*hauteur*10)/20,paint); 
for(int i=-3;i<=3;i++)canvas.drawPoint((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20+i*uni,paint);
paint.setStrokeWidth(12);
canvas.drawPoint((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20,paint);*/ 
}
if(numpie==-1||numpie==2||numpie==3||numpie==4){
float uni=540/14;
float longueurpie=12*uni;
float anglecorps=-(float)Math.toDegrees(Math.atan2(4*uni,longueurpie)); 
canvas.scale(0.5f,0.5f,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// translation d'ajustement:bas pattes = niveau le plus bas 
canvas.translate(0,-4*uni);
canvas.rotate(anglecorps,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
// tête 
paint.setStrokeWidth(9);
float tetepie=uni; 
paint.setColor(Color.GREEN);
canvas.drawCircle((float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20,uni,paint);
// antennes 
paint.setColor(Color.rgb(0,155,0));
paint.setStrokeWidth(5);
canvas.drawLine((float)(xpie*largeur*10)/20+uni-uni/2,(float)(ypie*hauteur*10)/20-uni/2,(float)(xpie*largeur*10)/20+uni-uni/2-uni/4,(float)(ypie*hauteur*10)/20-3*uni/2,paint);
canvas.drawLine((float)(xpie*largeur*10)/20+uni+3*uni/4,(float)(ypie*hauteur*10)/20-uni/2,(float)(xpie*largeur*10)/20+2*uni,(float)(ypie*hauteur*10)/20-3*uni/2,paint);
paint.setColor(Color.rgb(240,240,240));
canvas.drawRect((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+2*uni,(float)(ypie*hauteur*10)/20+uni,paint); 
// yeux 
paint.setStrokeWidth(7);
canvas.drawPoint((float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20-uni/2,paint);
canvas.drawPoint((float)(xpie*largeur*10)/20+uni+uni/2,(float)(ypie*hauteur*10)/20-uni/2,paint); 
paint.setColor(Color.BLACK); 
// bec dessous fermé en 2, ouvert ou semi-ouvert en 3-4
paint.setStrokeWidth(3); 
if(numpie==3||numpie==2||numpie==-1)for(int i=0;i<11;i++)canvas.drawLine((float)(xpie*largeur*10)/20+uni+i*uni/10,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+3*uni,(float)(ypie*hauteur*10)/20+uni,paint); 
if(numpie==4)for(int i=0;i<11;i++)canvas.drawLine((float)(xpie*largeur*10)/20+uni+i*uni/10,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+3*uni,(float)(ypie*hauteur*10)/20+0.5f*uni,paint);
if(numpie==3||numpie==4||numpie==-1){
// bec dessus ouvert ou semi-ouvert 
canvas.scale(1,-1,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
if(numpie==3||numpie==-1)for(int i=0;i<11;i++)canvas.drawLine((float)(xpie*largeur*10)/20+uni+i*uni/10,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+3*uni,(float)(ypie*hauteur*10)/20+uni,paint);
if(numpie==4)for(int i=0;i<11;i++)canvas.drawLine((float)(xpie*largeur*10)/20+uni+i*uni/10,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+3*uni,(float)(ypie*hauteur*10)/20+0.5f*uni,paint);
canvas.scale(1,-1,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
}
// corps 
paint.setColor(Color.BLACK);
paint.setStrokeWidth(3);
for(int i=0;i<11;i++)canvas.drawLine((float)(xpie*largeur*10)/20-longueurpie,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20+i*uni/10,paint);
canvas.drawLine((float)(xpie*largeur*10)/20-longueurpie,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20+2*uni,paint);
canvas.drawLine((float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20,(float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20+2*uni,paint);
// pattes
// rotation pour ajuster pattes au corps
canvas.rotate(-anglecorps/2,(float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20+2*uni);
for(int i=0;i<21;i++)canvas.drawLine((float)(xpie*largeur*10)/20-uni,(float)(ypie*hauteur*10)/20+4*uni,(float)(xpie*largeur*10)/20-uni+i*uni/10,(float)(ypie*hauteur*10)/20+2*uni,paint);
canvas.drawLine((float)(xpie*largeur*10)/20-uni,(float)(ypie*hauteur*10)/20+4*uni,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20+4*uni,paint);
canvas.translate(-uni,0);
for(int i=0;i<21;i++)canvas.drawLine((float)(xpie*largeur*10)/20-uni,(float)(ypie*hauteur*10)/20+4*uni,(float)(xpie*largeur*10)/20-uni+i*uni/10,(float)(ypie*hauteur*10)/20+2*uni,paint);
canvas.drawLine((float)(xpie*largeur*10)/20-uni,(float)(ypie*hauteur*10)/20+4*uni,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20+4*uni,paint);
canvas.translate(uni,0);
canvas.rotate(anglecorps/2,(float)(xpie*largeur*10)/20+uni,(float)(ypie*hauteur*10)/20+2*uni);
if(numpie==3||numpie==-1||numpie==4){
// Zigzag qd bec ouvert ou semi-ouvert
float ouvert=0;
if(numpie==4)ouvert=0.5f*uni;
paint.setColor(Color.RED);
for(int i=0;i<3;i++){
paint.setStrokeWidth(3+2*i);
canvas.drawLine((float)(xpie*largeur*10)/20+2*uni+ouvert+(float)Math.pow(2,i-1)*uni,(float)(ypie*hauteur*10)/20+(float)Math.pow(2,i-2)*uni,(float)(xpie*largeur*10)/20+2*uni+ouvert+(float)Math.pow(2,i)*uni,(float)(ypie*hauteur*10)/20-(float)Math.pow(2,i-1)*uni,paint);
canvas.drawLine((float)(xpie*largeur*10)/20+2*uni+ouvert+(float)Math.pow(2,i)*uni,(float)(ypie*hauteur*10)/20-(float)Math.pow(2,i-1)*uni,(float)(xpie*largeur*10)/20+2*uni+ouvert+(float)Math.pow(2,i)*uni,(float)(ypie*hauteur*10)/20+(float)Math.pow(2,i-1)*uni,paint);
}
// affichage mot pour verif.,supprimé pour plus de place à l'imagination... 
// paint.setTextSize(60);
// if(numpie==-1)canvas.drawText("Krakat",(float)(xpie*largeur*10)/20+6.5f*uni,(float)(ypie*hauteur*10)/20+uni/2,paint);
// if(mot.equals("")==false)canvas.drawText(mot,(float)(xpie*largeur*10)/20+6.5f*uni+ouvert,(float)(ypie*hauteur*10)/20+uni/2,paint);
}
// transformations inverses,pour retrouver repère initial
canvas.rotate(-anglecorps,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20);
canvas.translate(0,4*uni);
canvas.scale(2f,2f,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20); 
// repére
/* paint.setColor(Color.BLUE); 
paint.setStrokeWidth(7);
for(int i=-11;i<=4;i++)canvas.drawPoint((float)(xpie*largeur*10)/20+i*uni,(float)(ypie*hauteur*10)/20,paint); 
for(int i=-3;i<=3;i++)canvas.drawPoint((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20+i*uni,paint);
paint.setStrokeWidth(12);
canvas.drawPoint((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20,paint);
canvas.drawPoint((float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20-3*uni,paint);
canvas.drawPoint((float)(1*largeur*10)/20,(float)(15*hauteur*10)/20,paint);
canvas.drawPoint((float)(19*largeur*10)/20,(float)(15*hauteur*10)/20,paint);*/
} 
// en cas d'instructions ignorées,enlever puis remettre //
// if(numpie==1)canvas.drawText("fmo1"+anglepie,(float)(xpie*largeur*10)/20,(float)(ypie*hauteur*10)/20,paint);
}
}

class Dessin extends View{
private int hpts;
private int largeur;
int imax;
private int[][] couleur;
private float[][] pts;
private int[] lgs;
private long[] tps;
private float linmax;
public Dessin(Context context){
super(context); 
}
public void setpoint(int hpts,int largeur,int imax,int[][] couleur,float[][] pts,int[] lgs,long[] tps,float linmax){ 
this.hpts=hpts;
this.largeur=largeur;
this.imax=imax; 
this.couleur=couleur;
this.pts=pts; 
this.lgs=lgs;
this.tps=tps; 
this.linmax=linmax; 
}
@Override
protected void onDraw(Canvas canvas)
{
super.onDraw(canvas); 
Paint paint = new Paint();
paint.setTextSize(30);
paint.setStrokeWidth(1);
paint.setColor(Color.BLACK);
// graduations écran horiz.
/* for(int i=hpts;i<=hpts+27*8;i+=27){ 
canvas.drawLine(30,i,960,i,paint); 
float y=((float)-linmax/(27*4)*(i-27*4-hpts)) ; 
canvas.drawText((String.format("%.1f",Math.abs(y))),0,i+10,paint); 
}*/

for(int i=0;i<imax;i++){ 
paint.setStrokeWidth(5);
if(i%10==0){
String legs=String.format("%.1f",(float)lgs[i]/1000); 
String teps=String.format("%.3f",(float)tps[i]/1000);
paint.setColor(Color.BLACK);
canvas.drawText(legs,(i+1)*10-legs.length()*6,(hpts/2)*10+(hpts/2)*9,paint); 
canvas.drawText(teps,(i+1)*10-teps.length()*6,(hpts/2)*10+(hpts/2)*10,paint);
paint.setStrokeWidth(9); 
} 
for(int k=0;k<pts.length;k++){
paint.setColor(couleur[k][i]);
paint.setStrokeWidth(1);
canvas.drawLine(pts[k][4*i],pts[k][4*i+1]+(hpts/2)*10,pts[k][4*i+2],pts[k][4*i+3]+(hpts/2)*10,paint);
paint.setStrokeWidth(5); 
canvas.drawPoint(pts[k][4*i],pts[k][4*i+1]+(hpts/2)*10,paint);
} 
paint.setColor(Color.BLACK);
if(i%10==0)paint.setStrokeWidth(9);
if(pts.length==1)
canvas.drawPoint((i+1)*10,(hpts/2)*10+(hpts/2)*4,paint);
else canvas.drawPoint((i+1)*10,(hpts/2)*10+(hpts/2)*9,paint);
} 
} 
}

public class MainActivity extends Activity implements OnInitListener, SensorEventListener {
RelativeLayout contenant;
TextView[] tv;
TextView tvl;
    SensorManager sensorManager;
    Sensor accelerometer;
private Vibrator vib;
int n;
float[]diff;
ArrayList[] listval;
ArrayList[] listdiff;
Tdvals tdiff;
String str;
int p;
long ti;
int q;
int r;
String sttuni;
float seuil;
int qmax;
int somq;
int nq;
String[]s;
int h;
boolean plein;
long duret;
String sduret;
float xminr;
float xmaxr;
float dj;
float[]gen;
int k;
ArrayList laz;
int nbsigR;
String[]sg;
String[]st;
String sr;
String snr;
String sgen;
int typeR;
float[]sigNR;
AudioRecord ecoute;
AudioTrack joue;
// AudioManager am supprimé:à l'origine du bruit d'ecoute
int tolec;
int i;
float[][]pts;
int[]lgs;
long[]tps; 
short[]linecout; 
short[]linjoue;
int taille;
int newposition;
int shortlus;
float linmax;
Dessin d;
int te;
long tl;
int positionprec;
int[][]couleur;
int[]colore;
String[] repR; 
String[] repN;
int imax;
int tj;
int somfaz;
int somfaz2;
int somfaz3;
float[]linfreqjou;
float[]linfreq2jou;
float[]linfreq3jou;
boolean finlec;
int hauteur;
int largeur;
boolean vertical;
Display orientecran;
String s1,s2;
int rangfreq;
int rangampli;
int nbmots;
float[]mot;
String[]texte;
TextToSpeech tts;
boolean parle;
int indexmot;
Locale langue;
float[]pitch;
float[]rate;
int[]pause;
int tp;
Locale[]Langues;
SpannableString spatientetm;
SpannableString spatexter;
String langage;
int numpie;
Jakapie jakasso;
int xpie;
int ypie;
long instanpie;
boolean starton;
boolean pique;
boolean avance;
int anglepie;
int dxpie;
int dypie;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState); 
requestWindowFeature(Window.FEATURE_NO_TITLE);
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
WindowManager.LayoutParams.FLAG_FULLSCREEN);
getWindow().addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON); 
orientecran=((WindowManager) getSystemService(WINDOW_SERVICE)).getDefaultDisplay();
contenant=new RelativeLayout(this);
setContentView(contenant);
// orientation ecran vertical si rot0 ou 180, ou horizontal si 90 ou 270 
if(orientecran.getRotation()==Surface.ROTATION_0||orientecran.getRotation()==Surface.ROTATION_180)vertical=true;
else vertical=false; 
if(vertical){
hauteur=96;
largeur=54;
}
else{
hauteur=54;
largeur=96;
}
tvl=new TextView(this);
RelativeLayout.LayoutParams plt=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
// tvl à gauche qd colonnes params,à droite sinon  
if(vertical)plt.setMargins(430,375,0,0);
else plt.setMargins(0,375,0,0);
tvl.setLayoutParams(plt); 
contenant.addView(tvl);
tv=new TextView[8];
tv[0]=new TextView(this);
RelativeLayout.LayoutParams pt=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
pt.setMargins(430,0,0,0);
tv[0].setLayoutParams(pt); 
contenant.addView(tv[0]);
// tv6 et 7 pour affichage mots 
tv[6]=new TextView(this);
RelativeLayout.LayoutParams psix=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
// tv[6] à gauche qd colonnes params 
if(vertical)psix.setMargins(100,0,0,0);
else psix.setMargins(0,0,0,0);
tv[6].setLayoutParams(psix); 
contenant.addView(tv[6]);
tv[7]=new TextView(this);
RelativeLayout.LayoutParams pset=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
// tv[7] à gauche qd colonnes params 
if(vertical)pset.setMargins(200,0,0,0);
else pset.setMargins(400,0,0,0);
tv[7].setLayoutParams(pset); 
contenant.addView(tv[7]);
// affichage erreur 
tv[5]=new TextView(this);
RelativeLayout.LayoutParams pc=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
pc.setMargins(10,250,0,0); 
tv[5].setLayoutParams(pc); 
contenant.addView(tv[5]);
tv[4]=new TextView(this);
RelativeLayout.LayoutParams pdf=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
pdf.setMargins(30,0,0,0); 
tv[4].setLayoutParams(pdf); 
contenant.addView(tv[4]);
// affichage verif. params 3-28 sons
/* tv[1]=new TextView(this);
RelativeLayout.LayoutParams px=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
px.setMargins(400,0,0,0); 
tv[1].setLayoutParams(px); 
contenant.addView(tv[1]);
tv[2]=new TextView(this);
RelativeLayout.LayoutParams py=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
py.setMargins(593,0,0,0); 
tv[2].setLayoutParams(py); 
contenant.addView(tv[2]);
tv[3]=new TextView(this);
RelativeLayout.LayoutParams pz=new RelativeLayout.LayoutParams
(RelativeLayout.LayoutParams.WRAP_CONTENT,
RelativeLayout.LayoutParams.WRAP_CONTENT);
pz.setMargins(770,0,0,0); 
tv[3].setLayoutParams(pz); 
contenant.addView(tv[3]); */
        sensorManager = (SensorManager) getSystemService(this.SENSOR_SERVICE); 
        accelerometer = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER); 
// message en cas d'absence d'acceleromètre 
if(accelerometer==null)tv[5].setText("Désolé,il n'y a pas de capteur accéléromètre sur votre tel.");
// else tv[5].setText("capteur accéléromètre installé."); 
sensorManager.registerListener(this, accelerometer, SensorManager.SENSOR_DELAY_GAME);
vib=(Vibrator)getSystemService(this.VIBRATOR_SERVICE);
n=-1; 
p=-1;
diff=new float[3];
listval=new ArrayList[4];
listdiff=new ArrayList[4];
s=new String[4];
for(int k=0;k<4;k++){
listval[k]=new ArrayList();
listdiff[k]=new ArrayList(); 
if(k>0)s[k-1]="";
}
tdiff=new Tdvals();
str=""; 
sttuni="";
seuil=0.01f; 
plein=false;
gen=new float[4];
sgen="";
sr="";
snr="";
sg=new String[4];
sg[0]="nb";
sg[1]="tL";
sg[2]="cf";
sg[3]="tR";
st=new String[12];
st[0]="Ty";
st[1]="Xd";
st[2]="Xf";
st[8]=" Fa";
st[6]=" Pe";
st[7]=" Vi";
st[3]=" Fq";
st[9]=" Ty";
st[4]=" Ap";
st[5]=" Of";
st[10]=" Ym";
st[11]=" YM";
sduret="0.0";
finlec=false;
parle=true;
tvl.setText("T"); 
tolec=16000; 
s1="";
s2=""; 
// 20 langages choisis et téléchargés ds données vocales,params tel. 
Locale coreen=new Locale("ko","KR");
Locale espagnol=new Locale("es","ES");
Locale filipin=new Locale("fil","PH");
Locale hindou=new Locale("hi","IN");
Locale indonésien=new Locale("in","ID");
Locale brésilien=new Locale("pt","BR");
Locale russe=new Locale("ru","RU");
Locale finlandais=new Locale("fi","FI");
Locale danois=new Locale("da","DK");
Locale turc=new Locale("tr","TR");
Locale viet=new Locale("vi","VN"); 
Locale tcheque=new Locale("cs","CZ");
Locale nepalais=new Locale("ne","NP");
Locale hongrois=new Locale("hu","HU");
Locale cingalais=new Locale("si","LK");
Langues=new Locale[]{Locale.GERMANY,Locale.US,Locale.CHINA,coreen,espagnol,filipin,Locale.FRANCE,
hindou,indonésien,Locale.JAPAN,brésilien,russe,danois,finlandais,turc,viet,tcheque,nepalais,hongrois,cingalais};
// affichage orientation:0 ou 2 en vertical,1 ou 3 en horiz. 
// tv[5].setText(Integer.toString(orientecran.getRotation())+" "+Integer.toString(Surface.ROTATION_0)+" "+Integer.toString(Surface.ROTATION_90)+" "+Integer.toString(Surface.ROTATION_180)+" "+Integer.toString(Surface.ROTATION_270));
// tolec=32000->2tolec=64000 pas supporté
d=new Dessin(this);
contenant.addView(d); 
jakasso=new Jakapie(this); 
contenant.addView(jakasso);
// essais cadrage 
xpie=10;
ypie=10;
// pie d'essai 
/* Jakapie jakassobis=new Jakapie(this); 
jakassobis.setpie(hauteur,largeur,-1,xpie,ypie,0,"");
contenant.addView(jakassobis);*/
starton=false;
xpie=0;
ypie=10;
avance=true;
pique=true;
// thread obligé pour l'anim contenant.post+Dessin
(new Thread() {
@Override
public void run() { 
try{
ecoutejou(); 
}catch(final Throwable t){
tv[5].post(new Runnable() {
public void run() {
tv[5].setText("fin"+t.getMessage()); 
}
}); 
}
}
}).start();
    }
public void coordopie(){
// xpie 
if(avance==true){
if(xpie<=20){
dxpie=1+chiffret(8,tdiff.getT())/2;
xpie+=dxpie; 
}
else{ 
xpie=19;
avance=false; 
}
}
else{
if(xpie>=-1){
dxpie=1+chiffret(8,tdiff.getT())/2;
xpie-=dxpie; 
}
else{ 
xpie=0;
avance=true; 
}
}
// ypie 
if(pique==true){
if(ypie<=21){
dypie=1+chiffre(3,tdiff.getF()[1],333);
ypie+=dypie; 
}
else{
ypie=20;
pique=false;
}
}
else{
if(ypie>=0){
dypie=1+chiffre(3,tdiff.getF()[1],333);
ypie-=dypie; 
}
else{
ypie=1;
pique=true;
}
}
// calcul anglepie
if(avance==true){
if(pique==true)anglepie=(int)((float)Math.toDegrees(Math.atan2(dxpie,dypie)));
else anglepie=(int)(360-(float)Math.toDegrees(Math.atan2(dxpie,dypie)));
}
else{
// anglepie qui recule=-modulo anglepie qui avance
if(pique==true)anglepie=(int)(-(float)Math.toDegrees(Math.atan2(dxpie,dypie)));
else anglepie=(int)(-360+(float)Math.toDegrees(Math.atan2(dxpie,dypie)));
} 
}

@Override
public void onInit(int status) { 
if(status == TextToSpeech.SUCCESS) { 
tts.setOnUtteranceProgressListener(new UtteranceProgressListener(){
@Override
public void onStart(String s){
contenant.post(new Runnable() {
public void run() {
starton=true; 
if(indexmot<texte.length){
if(indexmot==0){
// pie au sol
xpie=(int)(xpie+(System.currentTimeMillis()-duret)/1000)%20;
// limites pour voir la pie qui parle
if(xpie>15||xpie<6)xpie=6;
ypie=20;
}
if(indexmot%2==0)jakasso.setpie(hauteur,largeur,4,xpie,ypie,0,texte[indexmot]);
if(indexmot%2==1)jakasso.setpie(hauteur,largeur,3,xpie,ypie,0,texte[indexmot]);
setContentView(contenant); 
indexmot++; 
} 
}
});
tv[5].post(new Runnable() {
public void run() {
tv[5].setText(""); 
}
}); 
}
@Override
public void onDone(String s){ 
tv[5].post(new Runnable() {
public void run() {
if(tts.isSpeaking()==false){
// affichage verif. fin texte 
// tv[5].setText("finblabla"+Arrays.toString(texte));
parle=true;
starton=false;
plein=false;
tts.stop();
tts.shutdown();
} 
}
}); 
}
@Override
public void onError(String s){
}
}); 
Bundle params = new Bundle();
// principe des intents avec clé à revoir 
params.putString(TextToSpeech.Engine.KEY_PARAM_UTTERANCE_ID,""); 
String attendmot="";
// essai avec langue manquante 
// langue=new Locale("ku");
if(tts.isLanguageAvailable(langue)!=1){
langue=tts.getDefaultLanguage();
attendmot="le langage:"+langue.getDisplayLanguage()+"\r\n"+
"n'est pas installé"+"\r\n"+
"sur votre tel."+"\r\n"+
"Pour l'installer:"+"\r\n"+ 
"Params,Langue"+"\r\n"+
"synthèse vocale"+"\r\n"+
"TTS(Google ou x)"+"\r\n"+
"données vocales"+"\r\n"+
"Téléch.langage."+"\r\n"+
"Le langage installé"+"\r\n"+
"par défaut est:"+tts.getDefaultLanguage().getDisplayLanguage()+"\r\n";
}
attendmot+="Veuillez patienter, mon "+langue.getDisplayLanguage()+" est un peu rouillé !";
spatexter=new SpannableString(attendmot);
spatexter.setSpan(new StyleSpan(Typeface.BOLD),0,attendmot.length(),Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
tv[5].setText(spatexter);
tts.setLanguage(langue);
for(int i=0;i<texte.length;i++){ 
tts.setPitch(pitch[i]);
tts.setSpeechRate(rate[i]); 
tts.speak(texte[i],TextToSpeech.QUEUE_ADD,params,""); 
// null à la fin pour pause,fin avec speak,params
// peut bloquer si pause à la fin,d'où length-1
if(i<texte.length-1) tts.playSilentUtterance(pause[i],tts.QUEUE_ADD,null);
}
}
}
public float transforms13(int e,int tauxech,float faz,float per,float vi,float fr,float ty,float amp,float off,float yd,float yf){ 
float trs=0; 
try{
if((e+faz)%((per+vi)*tauxech/fr)<per*tauxech/fr){
if(ty==1) 
trs=amp*(float)Math.sin((double)2*Math.PI/tauxech*fr*((e+faz)%((per+vi)*tauxech/fr)))+off; 
if(ty==2){
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/4)
trs=4*amp/(tauxech/fr)*(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr))+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/4
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<3*(tauxech/fr)/4)
trs=-4*amp/(tauxech/fr)*(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr))+2*amp+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=3*(tauxech/fr)/4)
trs=4*amp/(tauxech/fr)*(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr))-4*amp+off;
}
if(ty==3){
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/2)
trs=amp+off;
else trs=-amp+off;
}
if(ty==4) {
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/2)
trs=2*amp*(float)Math.sqrt(1-(float)3/4*Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-1),2))-amp+off; 
else trs=-2*amp*(float)Math.sqrt(1-(float)3/4*Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-3),2))+amp+off; 
}
if(ty==5){
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/4)
trs=-2*amp*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)),2))+2*amp+off; 
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/4
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/2)
trs=-2*amp*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-2),2))+2*amp+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/2
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<3*(tauxech/fr)/4)
trs=2*amp*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-2),2))-2*amp+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=3*(tauxech/fr)/4)
trs=2*amp*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-4),2))-2*amp+off; 
if(trs>amp)trs=amp+off;
if(trs<-amp)trs=-amp+off;
}
if(ty==6){
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/4)
trs=-2*amp*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)),2))+2*amp+off; 
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/4
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/2)
trs=2*amp*(float)Math.sqrt(1-(float)3/4*Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-1),2))-amp+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/2
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<3*(tauxech/fr)/4)
trs=-2*amp*(float)Math.sqrt(1-(float)3/4*Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-3),2))+amp+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=3*(tauxech/fr)/4)
trs=2*amp*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/4)-4),2))-2*amp+off;
if(trs>amp)trs=amp+off;
if(trs<-amp)trs=-amp+off;
}
if(ty==7){
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/8)
trs=-amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)),2))+amp/2+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/8
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<3*(tauxech/fr)/8)
trs=amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)-2),2))+amp/2+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/4
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<3*(tauxech/fr)/8)
trs=amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)-2),2))+amp/2+off; 
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=3*(tauxech/fr)/8
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<(tauxech/fr)/2)
trs=-amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)-4),2))+amp/2+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=(tauxech/fr)/2
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<5*(tauxech/fr)/8)
trs=amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)-4),2))-amp/2+off;
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=5*(tauxech/fr)/8
   &&((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)<7*(tauxech/fr)/8)
trs=-amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)-6),2))-amp/2+off; 
if(((e+faz)%((per+vi)*tauxech/fr))%(tauxech/fr)>=7*(tauxech/fr)/8)
trs=amp/2*(float)Math.sqrt(1-(float)Math.pow((double)(((e+faz)%((per+vi)*tauxech/fr)%(tauxech/fr))/((tauxech/fr)/8)-8),2))-amp/2+off;
} 
}
else{
if(off!=0)trs=off;
else trs=0.1f; 
}
if(trs<yd) trs=yd;
if(trs>yf) trs=yf; 
}catch(final Throwable t){
tv[5].post(new Runnable() {
public void run() {
tv[5].setText("trs13"+t.getMessage()); 
}
}); 
}
return trs;
}

public void ecoutejou(){ 
while(true){ 
if(plein==true){ 
float[]genlaz=new float[4];
genlaz=(float[])laz.get(0);
// ajustement sautille si ecran vertical
float sautille=0;
if(vertical)sautille=0.5f;
if(te>=1){
te=-1;
// toecout<tolec pour lecture accélérée
// toecout>tolec pour lecture ralentie 
// toecout max supporté=48000->tolec=tolecmax=16000;
float toecout=genlaz[2]*tolec; 
int bufMinR = AudioRecord.getMinBufferSize((int)toecout, AudioFormat.CHANNEL_IN_MONO, AudioFormat.ENCODING_PCM_16BIT);
// bufminr=3840 pour tolec=24000
// audiosource.voiceincom ou .mic
ecoute = new AudioRecord(MediaRecorder.AudioSource.MIC,(int)toecout, AudioFormat.CHANNEL_IN_MONO,
AudioFormat.ENCODING_PCM_16BIT,bufMinR); 
i=0; 
pts=new float[1][largeur*4];
lgs=new int[largeur];
tps=new long[largeur]; 
// int taille=5*8000; 
// durée écoute gen[3],modulée ds rempliz27 par gen[3],toecout=gen[3]*tolec
// if(gen[3]>0&&tj>=0)
// affichage verif. params sons 
// String patiente=sgen+"xm"+String.format("%.1f",xminr/1000)+"\r\n"+"xM"+String.format("%.1f",xmaxr/1000)+"\r\n"+"dj"+String.format("%.1f",dj/1000)+"\r\n"+"tm"+sduret+"\r\n"+"\r\n"+
// rappel:durée écoute=gen[3]/toécoute=gen[3]/(tolec*gen[2]) 
// "Je vous"+"\r\n"+"écoute:"+"\r\n"+"pendant"+"\r\n"+"environ"+"\r\n"+String.format("%.0f",gen[3]/(16000*gen[2]))+"secs"; 
String patiente="Je vous"+"\r\n"+"écoute:"+"\r\n"+"pendant"+"\r\n"+"environ"+"\r\n"+String.format("%.0f",gen[3]/(16000*gen[2]))+"secs";
spatientetm=new SpannableString(patiente);
spatientetm.setSpan(new StyleSpan(Typeface.BOLD),0,patiente.length(),Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
tv[0].post(new Runnable() {
public void run() { 
tv[0].setText(spatientetm);
}
}); 
int taille=(int)genlaz[3];
linecout=new short[taille]; 
newposition=0; 
positionprec=0;
shortlus=0; 
linmax=0.1f; 
int bruit=0;
couleur=new int[1][largeur];
for(int i=0;i<largeur;i++)couleur[0][i]=Color.rgb(255,0,0);
tl=System.currentTimeMillis();
ecoute.startRecording(); 
while (ecoute.getRecordingState()==AudioRecord.RECORDSTATE_RECORDING) { 
shortlus=ecoute.read(linecout,newposition,linecout.length/largeur);
newposition+=shortlus; 
if( linecout.length-newposition>=linecout.length/largeur){ 
if(i/4<largeur&&newposition-positionprec>=linecout.length/largeur){ 
lgs[i/4]=newposition-1;
tps[i/4]=System.currentTimeMillis()-tl; 
if(i%4==0) { 
// if(i==0) pts[0][0]=0;
if(i==0) pts[0][0]=10;
else pts[0][i]=pts[0][i-2]; 
i++;
}
if(i%4==1) { 
if(i==1){
// anim. sous forme de ligne
// pts[0][1]=27*k+1*27;
// anim sous forme de courbe,ecran vertical ou horizontal 
linmax=0.1f; 
// compensation bruit
if(Math.abs((float)(linecout[newposition-1]+bruit))>linmax)linmax=Math.abs((float)(linecout[newposition-1]+bruit));
pts[0][1]=(hauteur/2)*4-(float)(hauteur/2)*4/linmax*(float)(linecout[newposition-1]+bruit);
}
else pts[0][i]=pts[0][i-2]; 
i++;
}
if(i%4==2) { 
// pts[0][i]=10*((i/4+1));
pts[0][i]=10*((i/4)); 
i++;
}
if(i%4==3) { 
// couleur[0][i/4]=palette[0];
// anim. sous forme de ligne
// pts[0][i]=27*k+1*27;
// anim sous forme de courbe,ecran vertical ou horizontal 
// bruit enr. environ 900 
pts[0][i]=(hauteur/2)*4-(float)((hauteur/2)*4)/linmax*((float)(linecout[newposition-1]+bruit)); 
if(Math.abs((float)(linecout[newposition-1]+bruit))>linmax){ 
for(int l=1;l<=i;l+=2)
pts[0][l]=(hauteur/2)*4-(float)linmax/Math.abs((float)(linecout[newposition-1]+bruit))*((hauteur/2)*4-pts[0][l]); 
linmax=Math.abs((float)(linecout[newposition-1]+bruit));
} 
i++;
imax=i/4;
} 
positionprec=newposition;
}
d.setpoint(hauteur,largeur,imax,couleur,pts,lgs,tps,linmax); 
// pie sautille,200 en l'air,800 au sol(sur 2 lignes) 
if((System.currentTimeMillis()-duret)%1000<=200)jakasso.setpie(hauteur,largeur,2,(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20,17+sautille,0,"");
else jakasso.setpie(hauteur,largeur,2,(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20,18+sautille,0,""); 
contenant.post(new Runnable() {
public void run() { 
setContentView(contenant); 
}
}); 
}
else { 
ecoute.stop();
ecoute.release(); 
} 
} 
//  compensation bruit enr.à vide 
for(int c=0;c<linecout.length;c++)
linecout[c]+=bruit; 
// affichage après écoute 
/* tv[5].post(new Runnable() {
public void run() { 
tv[5].setText("finec"+Integer.toString(ecoute.getRecordingState())+" "+Integer.toString(ecoute.getState())+"\r\n"); 
}
}); */ 
}
if(tj>=1){
tj=-1;
final int bufMinT = AudioTrack.getMinBufferSize(tolec, AudioFormat.CHANNEL_OUT_MONO, AudioFormat.ENCODING_PCM_16BIT);
// bufmint=3072 pour tolec=24000 
// audiomanager.modeincom ou stream music
joue = new AudioTrack(AudioManager.STREAM_MUSIC, tolec, AudioFormat.CHANNEL_OUT_MONO,
  AudioFormat.ENCODING_PCM_16BIT, bufMinT, AudioTrack.MODE_STREAM);       
int tauxech=tolec; 
i=0;
pts=new float[(int)genlaz[0]][largeur*4];
lgs=new int[largeur];
tps=new long[largeur]; 
couleur=new int[pts.length][largeur]; 
newposition=0;
positionprec=newposition; 
taille=(int)genlaz[1];
linjoue=new short[taille]; 
try{ 
xpie=(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20;
duret=System.currentTimeMillis();
for(int k=1;k<=(int)genlaz[0];k++){ 
// affichage verif.params sons
// String patiente=sgen+"xm"+String.format("%.1f",xminr/1000)+"\r\n"+"xM"+String.format("%.1f",xmaxr/1000)+"\r\n"+"dj"+String.format("%.1f",dj/1000)+"\r\n"+"tm"+sduret+"\r\n"+"\r\n"+ 
// "Veuillez"+"\r\n"+"patienter:"+"\r\n"+"j'intègre"+"\r\n"+"beaucoup"+"\r\n"+"de données !"+"\r\n"+k+"signaux traités"+"\r\n"+"sur:"+(int)genlaz[0]; 
String patiente="Veuillez"+"\r\n"+"patienter:"+"\r\n"+"j'intègre"+"\r\n"+"beaucoup"+"\r\n"+"de données !"+"\r\n"+k+"signaux traités"+"\r\n"+"sur:"+(int)genlaz[0]; 
spatientetm=new SpannableString(patiente);
spatientetm.setSpan(new StyleSpan(Typeface.BOLD),0,patiente.length(),Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
tv[0].post(new Runnable() {
public void run() { 
tv[0].setText(spatientetm);
}
});
// pie au sol(sur 2 lignes) 
if((System.currentTimeMillis()-duret)%1000<=500)jakasso.setpie(hauteur,largeur,2,(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20,18+sautille,0,"");
// intégration des données trop long: 2 états inutiles 
// else jakasso.setpie(hauteur,largeur,2,(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20,18,""); 
contenant.post(new Runnable() {
public void run() { 
setContentView(contenant);
}
});
float[]siglaz=new float[34];
siglaz=(float[])laz.get(k); 
// int r=(int)xdebut[k]; 
int r=(int)siglaz[1];
// amplifaz<=1
if(siglaz[4]<=1){
// e<xfin[k] 
for(int e=r;e<siglaz[2];e++){
float floke=0;
// freqfaz coefficienté cfampli,signr[24],compris entre 0.05 et 1.05 
// floke=cfampli*transforms13(e,tauxech,fazfaz,periodefaz,videfaz,freqfaz,typfaz,amplifaz,offsetfaz,yminfaz,ymaxfaz); 
floke=siglaz[24]*transforms13(e-r,tauxech,siglaz[10],siglaz[8],siglaz[9],siglaz[3],siglaz[11],siglaz[4],siglaz[7],siglaz[12],siglaz[13]); 
// ajout des harmoniques freq2faz et freq3faz coefficientés cf2ampli et cf3ampli,compris entre 0.1 et 1.05
// floke+=cf2ampli*transforms13(e,tauxech,fazfaz,periodefaz,videfaz,freq2faz,typfaz,amplifaz,offsetfaz,yminfaz,ymaxfaz); 
floke+=siglaz[25]*transforms13(e-r,tauxech,siglaz[10],siglaz[8],siglaz[9],siglaz[5],siglaz[11],siglaz[4],siglaz[7],siglaz[12],siglaz[13]);
// floke=cf3ampli*transforms13(e,tauxech,fazfaz,periodefaz,videfaz,freq3faz,typfaz,amplifaz,offsetfaz,yminfaz,ymaxfaz); 
floke+=siglaz[26]*transforms13(e-r,tauxech,siglaz[10],siglaz[8],siglaz[9],siglaz[6],siglaz[11],siglaz[4],siglaz[7],siglaz[12],siglaz[13]);
if(Math.abs(siglaz[0])==4){
// ampliampli et offsetampli<=1;fait dans rempliz27
// amplifazmax+offsetfazmax=2->0.5*linecout,linecoutmax=16000 
// lecture inversée ou normale
if(siglaz[0]<0)floke*=0.5f*linecout[(linecout.length-1-e%linecout.length)%linecout.length];
else floke*=0.5f*linecout[e%linecout.length]; 
}
// floke*=transforms13(e,tauxech,fazampli,periodeampli,videampli,freqampli,typampli,ampliampli,offsetampli[k],yminampli,ymaxampli); 
floke*=transforms13(e-r,tauxech,siglaz[30],siglaz[28],siglaz[29],siglaz[22],siglaz[31],siglaz[23],siglaz[27],siglaz[32],siglaz[33]);
linjoue[e]+=(short)floke; 
}
}
else{
// linfreqjou=new float[(int)(tauxech/freqfaz)]; 
linfreqjou=new float[(int)(tauxech/siglaz[3])]; 
// linfreqjou=new float[(int)(tauxech/freqfaz)]; 
linfreq2jou=new float[(int)(tauxech/siglaz[3])];
// linfreqjou=new float[(int)(tauxech/freqfaz)]; 
linfreq3jou=new float[(int)(tauxech/siglaz[3])];
for(int e=0;e<linfreqjou.length;e++){
// linfreqjou[e]=transforms13(e,tauxech,fazfreq,1,0,freqfaz,typfaz,amplifaz,offsetfaz,yminfaz,ymaxfaz); 
linfreqjou[e]=transforms13(e,tauxech,siglaz[18],1,0,siglaz[3],siglaz[11],siglaz[4],siglaz[7],siglaz[12],siglaz[13]); 
// linfreq2jou[e]=transforms13(e,tauxech,fazfreq,1,0,freqfaz,typfaz,freq2faz=ampli2faz,offsetfaz,yminfaz,ymaxfaz); 
linfreq2jou[e]=transforms13(e,tauxech,siglaz[18],1,0,siglaz[3],siglaz[11],siglaz[5],siglaz[7],siglaz[12],siglaz[13]);
// linfreq3jou[e]=transforms13(e,tauxech,fazfreq,1,0,freqfaz,typfaz,freq3faz=ampli3faz,offsetfaz,yminfaz,ymaxfaz); 
linfreq3jou[e]=transforms13(e,tauxech,siglaz[18],1,0,siglaz[3],siglaz[11],siglaz[6],siglaz[7],siglaz[12],siglaz[13]);
}
somfaz=0;
somfaz2=0;
somfaz3=0;
for(int e=0;e<linfreqjou.length;e++){
// somfaz+=(int)(periodefaz*tauxech/linfreqjou[e])+(int)(videfaz*tauxech/offsetfaz); 
somfaz+=(int)(siglaz[8]*tauxech/linfreqjou[e])+(int)(siglaz[9]*tauxech/siglaz[7]); 
// somfaz2+=(int)(periodefaz*tauxech/linfreq2jou[e])+(int)(videfaz*tauxech/offsetfaz); 
somfaz2+=(int)(siglaz[8]*tauxech/linfreq2jou[e])+(int)(siglaz[9]*tauxech/siglaz[7]);
// somfaz+=(int)(periodefaz*tauxech/linfreq3jou[e])+(int)(videfaz*tauxech/offsetfaz); 
somfaz3+=(int)(siglaz[8]*tauxech/linfreq3jou[e])+(int)(siglaz[9]*tauxech/siglaz[7]);
}
// pour éviter division par zéro 
if((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz)==0)somfaz=10;
if((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2)==0)somfaz2=10;
if((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3)==0)somfaz3=10;
int edeb=0;
int edeb2=0;
int edeb3=0;
int cont=0;
int cont2=0;
int cont3=0;
// int poffe=(int)(tauxech/offsetfaz);
int poffe=(int)(tauxech/siglaz[7]);
int pe=(int)(tauxech/linfreqjou[0]); 
int pe2=(int)(tauxech/linfreq2jou[0]);
int pe3=(int)(tauxech/linfreq3jou[0]);
// e<xfin[k] 
for(int e=r;e<siglaz[2];e++){
// harmonique 1 coefficienté cfampli,compris entre 0.05 et 1.05 
float floke=0;
// (int)(periodegroup*somfaz)+(int)(videgroup*somfaz)
if((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz))<(int)(siglaz[16]*somfaz)){
if((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz))==0){
edeb=0;
cont=0;
// int poffe=(int)(tauxech/offsetfaz);
poffe=(int)(tauxech/siglaz[7]);
pe=(int)(tauxech/linfreqjou[0]);
}
// e>=edeb+(int)(periodefaz*pe)+(int)(videfaz*poffe)
if((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz))>=edeb+(int)(siglaz[8]*pe)+(int)(siglaz[9]*poffe)){
cont++;
edeb=(e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz));
pe=(int)(tauxech/linfreqjou[cont%linfreqjou.length]); 
}
//e>=edeb&&e<edeb+(int)(periodefaz*pe)+(int)(videfaz*poffe)
if((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz))>=edeb&&(e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz))<edeb+(int)(siglaz[8]*pe)+(int)(siglaz[9]*poffe)){
// e<edeb+(int)(periodefaz*pe)
if((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz))<edeb+(int)(siglaz[8]*pe)) 
// floke=cfampli*transforms13(e,tauxech,fazfaz-(edeb%pe),periodefaz,0,tauxech/pe,typgroup,ampligroup<=1,offsetgroup,ymingroup,ymaxgroup); 
floke=siglaz[24]*transforms13((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz)),tauxech,siglaz[10]-(edeb%pe),siglaz[8],0,tauxech/pe,siglaz[19],siglaz[14],siglaz[15],siglaz[20],siglaz[21]); 
// else floke=cfampli*transforms13(e,tauxech,fazfaz-(edeb+(int)(periodefaz*pe))%poffe,videfaz,0,tauxech/poffe,typgroup,ampligroup<=1,offsetgroup,ymingroup,ymaxgroup); 
else floke=siglaz[24]*transforms13((e-r)%((int)(siglaz[16]*somfaz)+(int)(siglaz[17]*somfaz)),tauxech,siglaz[10]-(edeb+(int)(siglaz[8]*pe))%poffe,siglaz[9],0,tauxech/poffe,siglaz[19],siglaz[14],siglaz[15],siglaz[20],siglaz[21]); 
}
}
else floke=0; 
// harmonique 2 coef2ampli compris entre 0.05 et 1.05
if((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2))<(int)(siglaz[16]*somfaz2)){
if((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2))==0){
edeb2=0;
cont2=0;
// int poffe=(int)(tauxech/offsetfaz);
poffe=(int)(tauxech/siglaz[7]);
pe2=(int)(tauxech/linfreq2jou[0]);
}
// e>=edeb+(int)(periodefaz*pe)+(int)(videfaz*poffe)
if((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2))>=edeb2+(int)(siglaz[8]*pe2)+(int)(siglaz[9]*poffe)){
cont2++;
edeb2=(e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2));
pe2=(int)(tauxech/linfreq2jou[cont2%linfreq2jou.length]); 
}
//e>=edeb&&e<edeb+(int)(periodefaz*pe)+(int)(videfaz*poffe)
if((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2))>=edeb2&&(e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2))<edeb2+(int)(siglaz[8]*pe2)+(int)(siglaz[9]*poffe)){
// e<edeb+(int)(periodefaz*pe)
if((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2))<edeb2+(int)(siglaz[8]*pe2)) 
// floke+=cf2ampli*transforms13(e,tauxech,fazfaz-(edeb2%pe2),periodefaz,0,tauxech/pe2,typgroup,ampligroup<=1,offsetgroup,ymingroup,ymaxgroup); 
floke+=siglaz[25]*transforms13((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2)),tauxech,siglaz[10]-(edeb2%pe2),siglaz[8],0,tauxech/pe2,siglaz[19],siglaz[14],siglaz[15],siglaz[20],siglaz[21]); 
// else floke+=cf2ampli*transforms13(e,tauxech,fazfaz-(edeb2+(int)(periodefaz*pe2))%poffe,videfaz,0,tauxech/poffe,typgroup,ampligroup<=1,offsetgroup,ymingroup,ymaxgroup); 
else floke+=siglaz[25]*transforms13((e-r)%((int)(siglaz[16]*somfaz2)+(int)(siglaz[17]*somfaz2)),tauxech,siglaz[10]-(edeb2+(int)(siglaz[8]*pe2))%poffe,siglaz[9],0,tauxech/poffe,siglaz[19],siglaz[14],siglaz[15],siglaz[20],siglaz[21]); 
}
}
else floke+=0;
// harmonique 3 coef3ampli compris entre 0.05 et 1.05
if((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3))<(int)(siglaz[16]*somfaz3)){
if((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3))==0){
edeb3=0;
cont3=0;
// int poffe=(int)(tauxech/offsetfaz);
poffe=(int)(tauxech/siglaz[7]);
pe3=(int)(tauxech/linfreq3jou[0]);
}
// e>=edeb3+(int)(periodefaz*pe3)+(int)(videfaz*poffe)
if((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3))>=edeb3+(int)(siglaz[8]*pe3)+(int)(siglaz[9]*poffe)){
cont3++;
edeb3=(e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3));
pe3=(int)(tauxech/linfreq3jou[cont3%linfreq3jou.length]); 
}
//e>=edeb3&&e<edeb3+(int)(periodefaz*pe3)+(int)(videfaz*poffe)
if((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3))>=edeb3&&(e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3))<edeb3+(int)(siglaz[8]*pe3)+(int)(siglaz[9]*poffe)){
// e<edeb3+(int)(periodefaz*pe3)
if((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3))<edeb3+(int)(siglaz[8]*pe3)) 
// floke+=cf3ampli*transforms13(e,tauxech,fazfaz-(edeb3%pe3),periodefaz,0,tauxech/pe3,typgroup,ampligroup<=1,offsetgroup,ymingroup,ymaxgroup); 
floke+=siglaz[26]*transforms13((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3)),tauxech,siglaz[10]-(edeb3%pe3),siglaz[8],0,tauxech/pe3,siglaz[19],siglaz[14],siglaz[15],siglaz[20],siglaz[21]); 
// else floke+=cf3ampli*transforms13(e,tauxech,fazfaz-(edeb3+(int)(periodefaz*pe3))%poffe,videfaz,0,tauxech/poffe,typgroup,ampligroup<=1,offsetgroup,ymingroup,ymaxgroup); 
else floke+=siglaz[26]*transforms13((e-r)%((int)(siglaz[16]*somfaz3)+(int)(siglaz[17]*somfaz3)),tauxech,siglaz[10]-(edeb3+(int)(siglaz[8]*pe3))%poffe,siglaz[9],0,tauxech/poffe,siglaz[19],siglaz[14],siglaz[15],siglaz[20],siglaz[21]); 
}
}
else floke+=0;
if(Math.abs(siglaz[0])==4){
// ampliampli et offsetampli<=1;fait ds rempliz27
// amplifazmax+offsetfazmax=2->0.5*linecout,linecoutmax=16000 
// lecture inversée ou normale
if(siglaz[0]<0)floke*=0.5f*linecout[(linecout.length-1-e%linecout.length)%linecout.length];
else floke*=0.5f*linecout[e%linecout.length]; 
} 
// floke*=transforms13(e,tauxech,fazampli,periodeampli,videampli,freqampli,typampli,ampliampli,offsetampli[k],yminampli,ymaxampli); 
floke*=transforms13(e-r,tauxech,siglaz[30],siglaz[28],siglaz[29],siglaz[22],siglaz[31],siglaz[23],siglaz[27],siglaz[32],siglaz[33]);
linjoue[e]+=floke; 
} 
}
}
}catch(final Throwable t){
tv[5].post(new Runnable() {
public void run() {
tv[5].setText("linjou"+Integer.toString((int)(somfaz*sigNR[16])+(int)(somfaz*sigNR[18]))+ t.getMessage()); 
}
}); 
}
// pie au sol,on fige xpie 
xpie=(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20;
// limites pour voir la pie qui chante,selon l'orientation de l'écran 
if(!vertical){
if(xpie<6||xpie>15)xpie=6;
}
else if(xpie<8||xpie>15)xpie=8;
shortlus=0; 
float[]linmak=new float[pts.length];
// linmax=0.1f; 
tl=System.currentTimeMillis();
// affichage verif.params sons 
/* String ceparti=sgen+"xm"+String.format("%.1f",xminr/1000)+"\r\n"+"xM"+String.format("%.1f",xmaxr/1000)+"\r\n"+"dj"+String.format("%.1f",dj/1000)+"\r\n"+"tm"+sduret+"\r\n"+"\r\n"+ 
"  Kraka"+"\r\n"+"  Sons !"; 
spatientetm=new SpannableString(ceparti);
spatientetm.setSpan(new StyleSpan(Typeface.BOLD),0,ceparti.length(),Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
tv[0].post(new Runnable() {
public void run() { 
tv[0].setText(spatientetm);
}
});*/
tv[0].post(new Runnable() {
public void run() { 
// efface message patience
tv[0].setText("");
}
});
joue.play();
while (joue.getPlayState()==AudioTrack.PLAYSTATE_PLAYING) { 
shortlus=joue.write(linjoue,newposition,linjoue.length/largeur);
newposition+=shortlus;
if( linjoue.length-newposition>=linjoue.length/largeur){ 
if(i/4<largeur&&newposition-positionprec>=linjoue.length/largeur){ 
lgs[i/4]=newposition-1;
tps[i/4]=System.currentTimeMillis()-tl; 
if(i%4==0) {
for(int k=1;k<=(int)genlaz[0];k++){ 
// pts[k-1][0]=10
if(i==0) pts[k-1][0]=0;
else pts[k-1][i]=pts[k-1][i-2];
}
i++;
}
if(i%4==1) {
for(int k=1;k<=(int)genlaz[0];k++){ 
if(i==1){
// anim. sous forme de ligne,ecran vertical ou horizontal
if(vertical)pts[k-1][1]=(hauteur/4)*(k-1)-(hauteur/2)*9-(hauteur/4);
else pts[k-1][1]=(hauteur/2-3)*(k-1)-(hauteur/2-3)*9-(hauteur/2-3);
// anim sous forme de courbe,écran horiz. 
// pts[k][1]=27*4;
/* if(!vertical){
linmax=0.1f; 
linmak[k-1]=0.1f; 
if(Math.abs(linjoue[newposition-1])>linmak[k-1]){
linmak[k-1]=Math.abs(linjoue[newposition-1]);
if(linmak[k-1]>linmax)linmax=linmak[k-1];
} 
pts[k-1][1]=27*4-(float)27*4/linmak[k-1]*linjoue[newposition-1];
} */
}
else pts[k-1][i]=pts[k-1][i-2];
}
i++;
}
if(i%4==2) {
for(int k=1;k<=(int)genlaz[0];k++) 
// pts[k-1][i]=10*((i/4+1));
pts[k-1][i]=10*((i/4)); 
i++;
}
if(i%4==3) { 
for(int k=1;k<=(int)genlaz[0];k++){
float[]siglaz=new float[34];
siglaz=(float[])laz.get(k);
// newposition>=(int)xdebut[k]&&newposition<xfin[k]
if(newposition>=(int)siglaz[1]&&newposition<siglaz[2]){
if(Math.abs(siglaz[0])==4){
if(siglaz[4]<=1){
if(siglaz[0]>0)couleur[k-1][i/4]=Color.rgb(255,0,0); 
else couleur[k-1][i/4]=Color.rgb(200,0,0);
}
else{
if(siglaz[0]>0)couleur[k-1][i/4]=Color.rgb(255,155,0); 
else couleur[k-1][i/4]=Color.rgb(200,155,0);
}
}
else{
if(siglaz[4]<=1)couleur[k-1][i/4]=Color.rgb(0,0,255);
else couleur[k-1][i/4]=Color.rgb(0,155,0);
}
}
// anim. sous forme de ligne,ecran vertical ou horizontal 
if(vertical){
// 96/4=24
pts[k-1][i]=(hauteur/4)*(k-1)-(hauteur/2)*9-(hauteur/4); 
if(k==40)pts[k-1][i]=(hauteur/4)*(k-1)-(hauteur/2)*9-(hauteur/4)-(hauteur/8);
}
else{
// 54/2=27 
pts[k-1][i]=(hauteur/2-3)*(k-1)-(hauteur/2-3)*10;
}
// anim sous forme de courbe,écran horiz. 
/* if(!vertical){
pts[k-1][i]=27*4-(float)(27*4)/linmak[k-1]*(linjoue[newposition-1]); 
if(Math.abs(linjoue[newposition-1])>linmak[k-1]){ 
for(int l=1;l<=i;l+=2) 
pts[k-1][l]=27*4-(float)linmak[k-1]/Math.abs(linjoue[newposition-1])*(27*4-pts[k-1][l]); 
linmak[k-1]=Math.abs(linjoue[newposition-1]);
if(linmak[k-1]>linmax)linmax=linmak[k-1];
}
} */
}
i++;
imax=i/4;
} 
positionprec=newposition;
}
d.setpoint(hauteur,largeur,imax,couleur,pts,lgs,tps,linmax); 
// pie au sol 
if(imax%2==0)jakasso.setpie(hauteur,largeur,4,xpie,ypie+sautille,0,"");
else jakasso.setpie(hauteur,largeur,3,xpie,ypie+sautille,0,"");
contenant.post(new Runnable() {
public void run() { 
setContentView(contenant); 
}
}); 
}
else { 
joue.stop();
joue.release(); 
}
} 
// affichage somfaz,linfreqjou 
/* tv[5].post(new Runnable() {
public void run() { 
tv[5].setText("finec,somfaz="+Integer.toString(somfaz)+"\r\n"+"finjo"+"\r\n"+Arrays.toString(linfreqjou)+"\r\n"); 
}
}); */
finlec=true;
}
} 
}
}

public void rempliz27(Tdvals tdiff){
try{
if(k==0){ 
// duret=System.currentTimeMillis(); 
if(h==0){
tv[0].setText("");
tv[7].setText("");
// affichage colonnes params sons 
// for(int c=1;c<=3;c++)tv[c].setText("");
for(int c=4;c<tv.length;c++)tv[c].setText("");
contenant.removeView(d);
d=new Dessin(this);
contenant.addView(d);
duret=System.currentTimeMillis();
instanpie=System.currentTimeMillis();
if(Math.signum(tdiff.getF()[1])>0)nbmots=0;
// si nbmots=0,chiffret8 et chiffre3 pas utilisés 
else nbmots=1+2*chiffre(3,tdiff.getF()[1],125)+chiffret(8,tdiff.getT())/5;
// sinon nbmots=1+2*[0-7]+[0-1]=[1-16] 
// affichage nbmots pour essai
// nbmots=3;
}
if(nbmots==0){
gen=new float[4]; 
// nb de signaux gen[0]:11+[0-29]en écran vertic.,13+[0-9] en horizontal 
if(vertical)gen[0]=11+chiffret(8,tdiff.getT())+10*chiffre(3,tdiff.getF()[1],333); 
else gen[0]=13+chiffret(8,tdiff.getT());
// toecout=gen[2]*tolec, le même pour tous les sigR
// au début gen[2]=1,change pour le 1er typer
gen[2]=1; 
laz=new ArrayList();
laz.add(0,gen);
k=1;
h=0;
nbsigR=0; 
sgen="";
sr="";
snr=""; 
repR=new String[(int)gen[0]]; 
repN=new String[(int)gen[0]]; 
for(int c=0;c<(int)gen[0];c++) {
repR[c]=""; 
repN[c]=""; 
}
} 
else{ 
if(h==0){
snr="";
gen=new float[nbmots+2];
gen[0]=nbmots;
}
if(h==1){
// 20 langues dispos dans langues,gen[1]:[0-19]
gen[1]=chiffret(8,tdiff.getT())*2+Math.signum(tdiff.getF()[1])*0.5f+0.5f;
langue=Langues[(int)gen[1]]; 
}
if(h>=2){
// nb lettres d'un mot:[1-10]
gen[h]=chiffret(8,tdiff.getT())+1; 
}
h++; 
if(h>=gen.length){ 
k=1;
h=0; 
laz=new ArrayList();
laz.add(0,gen);
sgen="nbmots:"+nbmots+" langue:"+langue.getDisplayCountry()+"\r\n";
// snr=langue.getDisplayCountry()+"\r\n";
} 
}
} 
if(nbmots==0){ 
if(h==0){ 
if(chiffret(8,tdiff.getT())>4)typeR=3;
else typeR=4; 
}
if(typeR!=4){
if(nbsigR==0){
xminr=0;
xmaxr=0;
dj=0;
gen[3]=0; 
}
}
if(h==0){
sigNR=new float[34];
sigNR[0]=typeR;
if(typeR!=4)repN[k-1]="N"+Integer.toString(k);
else{ 
nbsigR++; 
// signe pour lecture normale ou inversée 
sigNR[0]=typeR*Math.signum(tdiff.getF()[1]); 
repR[k-1]="R"+Integer.toString(k);
}
} 
laz.add(k,sigNR);
if(h<3){
if(h>0){ 
if(h==1){ 
// sigNR[h]=0; 
// début jeu[0.11*48000;480000] 
sigNR[h]=(int)((0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*48000*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],500))); 
}
if(h==2){ 
if(sigNR[0]!=4){ 
// sigNR[h]=3*16000; 
// fin jeu:début jeu+[0.11*480000;480000]
sigNR[h]=(int)((sigNR[1]+(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*480000)); 
}
else{
// sigNR[2]=3*16000;
// durée écoute modulée ensuite par gen[2],toecout=gen[2]*tolec
// fin écoute:début écoute+2*16000+[0.11*160000;160000] 
sigNR[h]=(int)((sigNR[1]+2*16000+(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*160000)); 
} 
// durée lecture 
if(sigNR[2]>gen[1])gen[1]=(int)sigNR[2]; 
if(typeR==4){
if(nbsigR==1){
xminr=sigNR[1];
xmaxr=sigNR[2];
if(chiffre(3,tdiff.getF()[1],143)+1==1)gen[2]=0.33333f; 
if(chiffre(3,tdiff.getF()[1],143)+1==2)gen[2]=0.5f;
if(chiffre(3,tdiff.getF()[1],143)+1==3)gen[2]=0.66667f;
if(chiffre(3,tdiff.getF()[1],143)+1==4)gen[2]=1;
if(chiffre(3,tdiff.getF()[1],143)+1==5)gen[2]=1.5f;
if(chiffre(3,tdiff.getF()[1],143)+1==6)gen[2]=2;
if(chiffre(3,tdiff.getF()[1],143)+1==7)gen[2]=3;
}
dureR(sigNR[1],sigNR[2]);
// durée écoute=gen[3],multipliée  par coeff gen[2],toecout=gen[2]*tolec 
gen[3]=(int)((xmaxr-xminr-dj)*gen[2]); 
}
}
}
if(typeR!=4){
if(h==0)sr+=repN[k-1]+"k"+Integer.toString(k)+" h"+Integer.toString(h)+st[h]+Float.toString(sigNR[h]);
else sr+=" h"+Integer.toString(h)+st[h]+String.format("%.1f",sigNR[h]/1000); 
}
else{
if(h==0)sr+=repR[k-1]+"k"+Integer.toString(k)+" h"+Integer.toString(h)+st[h]+Float.toString(sigNR[h]);
else sr+=" h"+Integer.toString(h)+st[h]+String.format("%.1f",sigNR[h]/1000);
}
}
else{ 
// freqfaz 
if(h==3){
// sigNR[h]=100; 
// freqfaz:[0.11*160-160]*10^[0-2]
rangfreq=chiffre(3,tdiff.getF()[1],333);
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*160*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],333)); 
} 
// amplifaz et rang 
if(h==4){ 
// sigNR[h]=1; 
// si chiffre(3,t,250)>0(3fois sur 4 modul faz),min:0.11*80,max:8000;
// sinon [0.0-0.95]
if(chiffre(3,tdiff.getF()[1],250)>0){ 
rangampli=chiffre(3,tdiff.getF()[1],250)-1;
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*80*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],250)-1);
}
else sigNR[h]=chiffret(8,tdiff.getT())*0.1f+Math.signum(tdiff.getF()[1])*0.025f+0.025f; 
}
// 2e harmonique:freq2faz 
if(h==5){ 
int nbh=0;
int nbdiv=0;
int nbmult=0;
if(sigNR[4]<=1){
// nbh=nb diviseurs de freqfaz >= min + nb multiples de freqfaz <=max -1 pour ne pas compter 2fois freq/1 et freq*1 
nbdiv=(int)(Math.floor(sigNR[3]/(0.11f*160*Math.pow(10,rangfreq))));
nbmult=(int)(Math.floor(160*Math.pow(10,rangfreq)/sigNR[3]))-1;
nbh=nbdiv+nbmult;
if(nbdiv!=nbmult){
if(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1<=nbdiv)sigNR[h]=sigNR[3]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[3]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
else{
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=sigNR[3]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[3]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
if(rangfreq==0)sigNR[h]*=10;
if(rangfreq==1)sigNR[h]*=0.1f;
if(rangfreq==2)sigNR[h]*=0.01f;
}
else{
// nbh=nb diviseurs de amplifaz >= min + nb multiples de amplifaz <=max -1 pour ne pas compter 2fois freq/1 et freq*1 
nbdiv=(int)(Math.floor(sigNR[4]/(0.11f*80*Math.pow(10,rangampli))));
nbmult=(int)(Math.floor(80*Math.pow(10,rangampli)/sigNR[4]))-1;
nbh=nbdiv+nbmult;
if(nbdiv!=nbmult){
if(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1<=nbdiv)sigNR[h]=sigNR[4]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[4]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
else{
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=sigNR[4]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[4]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
if(rangampli==0)sigNR[h]*=10;
if(rangampli==1)sigNR[h]*=0.1f;
if(rangampli==2)sigNR[h]*=0.01f;
}
// affichage params harmonik2 
// s1="rf"+Integer.toString(rangfreq)+"ra"+Integer.toString(rangampli)+"nbh"+Integer.toString(nbh)+"nbdiv"+Integer.toString(nbdiv)+"nbmu"+Integer.toString(nbmult)+"chif"+Integer.toString( (chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1))+"f1 "+Float.toString(sigNR[h]);
}
// 3e harmonique:freq3faz 
// s2=s1+"\r\n";
if(h==6){ 
int nbh=0;
int nbdiv=0;
int nbmult=0;
if(sigNR[4]<=1){
// nbh=nb diviseurs de freqfaz >= min + nb multiples de freqfaz <=max -1 pour ne pas compter 2fois freq/1 et freq*1 
nbdiv=(int)(Math.floor(sigNR[3]/(0.11f*160*Math.pow(10,rangfreq))));
nbmult=(int)(Math.floor(160*Math.pow(10,rangfreq)/sigNR[3]))-1;
nbh=nbdiv+nbmult;
if(nbdiv!=nbmult){
if(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1<=nbdiv)sigNR[h]=sigNR[3]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[3]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
else{
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=sigNR[3]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[3]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
if(rangfreq==0)sigNR[h]*=100;
if(rangfreq==1)sigNR[h]*=10;
if(rangfreq==2)sigNR[h]*=0.1f;
}
else{
// nbh=nb diviseurs de amplifaz >= min + nb multiples de amplifaz <=max -1 pour ne pas compter 2fois freq/1 et freq*1 
nbdiv=(int)(Math.floor(sigNR[4]/(0.11f*80*Math.pow(10,rangampli))));
nbmult=(int)(Math.floor(80*Math.pow(10,rangampli)/sigNR[4]))-1;
nbh=nbdiv+nbmult;
if(nbdiv!=nbmult){
if(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1<=nbdiv)sigNR[h]=sigNR[4]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[4]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
else{
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=sigNR[4]/(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1);
else sigNR[h]=sigNR[4]*(nbh-(chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1)+2);
}
if(rangampli==0)sigNR[h]*=100;
if(rangampli==1)sigNR[h]*=10;
if(rangampli==2)sigNR[h]*=0.1f;
}
// affichage params harmoniks 2 et 3 
// s2+="rf"+Integer.toString(rangfreq)+"ra"+Integer.toString(rangampli)+"nbh"+Integer.toString(nbh)+"nbdiv"+Integer.toString(nbdiv)+"nbmu"+Integer.toString(nbmult)+"chif"+Integer.toString((chiffre(3,tdiff.getF()[1],(int)(1000/nbh))+1))+"f2 "+Float.toString(sigNR[h]);
// tv[5].setText(s2);
} 
// offsetfaz
if(h==7){ 
if(sigNR[4]<=1){ 
// sigNR[h]=1f;
// offsetfaz compris entre -0.9875et0.9875
sigNR[h]=Math.signum(tdiff.getF()[1])*(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f); 
// pas de réajustement:au plus abs(offsetfaz+amplifaz)=2 
}
else{ 
// sigNR[h]=250;
// si ampfaz>1,offsetfaz doit être >ampfaz>=0 
// dans ce cas,offsetfaz-amplifaz pris >=1 pour être entendu 
// offsetfaz=amplifaz+[0.11*80-8000]
sigNR[h]=sigNR[4]+(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*80*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],333)); 
} 
}
// perfaz>0
if(h==8){
// sigNR[h]=1;
// choix de per compris entre 0.11 et 10,une fois sur 2 <=1
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*1*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],500)); 
}
// vidfaz
if(h==9){ 
// sigNR[h]=0;
// choix de vid compris entre 0 et 10,une fois sur 2 <=0.9875
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f);
else sigNR[h]=(1+chiffret(8,tdiff.getT())+chiffre(3,tdiff.getF()[1],125)*0.125f); 
}
// fazfaz
if(h==10){
// sigNR[h]=0;
// ds trs13,e+fazfaz modulés ensemble,
// choix de fazfaz variant comme e de signr[1] à signr[2]
// floor(log10(durée=a*10^k))donne son exposant k,avec durée min=16000
// fazfaz min:0.11*10a,max:durée
int expo=(int)Math.floor(Math.log10(sigNR[2]-sigNR[1]));
sigNR[h]=(int)((0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*(sigNR[2]-sigNR[1])*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],1000/(expo+1)-expo-1))); 
} 
// typfaz
if(h==11){
// sigNR[h]=1;
sigNR[h]=chiffre(3,tdiff.getF()[1],143)+1; 
}
// yminfaz
if(h==12){ 
// sigNR[h]=-33000;
sigNR[h]=sigNR[7]-sigNR[4]+Math.signum(tdiff.getF()[1])*(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f)*2*sigNR[4];
}
// ymaxfaz
if(h==13){ 
// sigNR[h]=33000;
// ymax=ymin+[0.1-1.0875]*2ampli
sigNR[h]=sigNR[12]+(0.1f+chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f)*2*sigNR[4];
}
//rappel: ampligroup<=1
if(h==14){
// sigNR[h]=1;
sigNR[h]=(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f); 
}
// offsetgroup
if(h==15){
//  rappel:offsetgroup compris entre -0.9875 et 0.9875 
// sigNR[h]=1;
sigNR[h]=Math.signum(tdiff.getF()[1])*(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f); 
// pas de réajustement:abs(offsetgroup+ampligroup=2) 
}
// pergroup
if(h==16){
// sigNR[h]=1;
// rappel:pergroup utilisé quand amplifaz>1
// choix de per compris entre 0.11 et 10,une fois sur 2 <=1
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*1*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],500)); 
}
// vidgroup
if(h==17){
// sigNR[h]=0;
// rappel:vidgroup utilisé quand amplifaz>1
// choix de vid compris entre 0 et 10,une fois sur 2 <=0.9875
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f);
else sigNR[h]=(1+chiffret(8,tdiff.getT())+chiffre(3,tdiff.getF()[1],125)*0.125f); 
}
// fazfreq
if(h==18){ 
// sigNR[h]=0;
// ds trs13,e+fazfreq modulés ensemble,
// choix de fazfreq variant de 0 à longueur de linfreqjou=(int)(tauxech/freqfaz)-1,
// fazfreq min:0.11*16,fazfreq max:16000 
sigNR[h]=(int)((0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*16*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],250))); 
}
// typgroup
if(h==19){
// sigNR[h]=1;
sigNR[h]=chiffre(3,tdiff.getF()[1],143)+1; 
} 
// ymingroup
if(h==20){
// sigNR[h]=-33000;
sigNR[h]=sigNR[15]-sigNR[14]+Math.signum(tdiff.getF()[1])*(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f)*2*sigNR[14];
}
// ymaxgroup
if(h==21){
// sigNR[h]=33000; 
// ymax=ymin+[0.1-1.0875]*2ampli
sigNR[h]=sigNR[20]+(0.1f+chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f)*2*sigNR[14]; 
}
// freqampli
if(h==22){
// sigNR[h]=100;
// min:0.11*1.6,max:tolec=1.6*10000; 
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*1.6f*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],200)); 
} 
// ampliampli
if(h==23){ 
if(typeR!=4){
// sigNR[h]=1600;
// min:0.11*1600,max:tolec=1600*10; 
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*1600*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],500)); 
}
else{
// si typr=4 ampliampli<=1 
// sigNR[h]=1; 
sigNR[h]=(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f);
}
}
// coefampli
if(h==24){
// coefampli:[0.1-1.05]
sigNR[h]=0.1f+chiffret(8,tdiff.getT())*0.1f+Math.signum(tdiff.getT())*0.025f+0.025f;
}
// coef2ampli
if(h==25){
// coef2ampli:[0.1-1.05]
sigNR[h]=0.1f+chiffret(8,tdiff.getT())*0.1f+Math.signum(tdiff.getT())*0.025f+0.025f;
}
// coef3ampli
if(h==26){
// coef3ampli:[0.1-1.05]
sigNR[h]=0.1f+chiffret(8,tdiff.getT())*0.1f+Math.signum(tdiff.getT())*0.025f+0.025f;
}
// offsetampli
if(h==27){ 
if(typeR!=4){ 
// sigNR[h]=1600; 
// min:abs(offsetampli)=0.11*1600,max1600*10 
sigNR[h]=Math.signum(tdiff.getF()[1])*(0.11f+chiffret(8,tdiff.getT())*0.89f/9*1600)*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],500));
}
else{ 
// sigNR[h]=1;
// amplitude max ecoute=15000->amplitude max jeu=(offsetamplimax+ampliamplimax)*15000,/2 ds ecoutejou
sigNR[h]=Math.signum(tdiff.getF()[1])*(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f);
// pas de réajustement: max abs(offsetampli+ampliampli)=2 
} 
}
// perampli
if(h==28){
// sigNR[h]=1; 
// choix de per compris entre 0.11 et 10,une fois sur 2 <=1
sigNR[h]=(0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*1*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],500)); 
}
// vidampli
if(h==29){
// sigNR[h]=0;
// choix de vid compris entre 0 et 10,une fois sur 2 <=0.9875
if(Math.signum(tdiff.getF()[1])<0)sigNR[h]=(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f);
else sigNR[h]=(1+chiffret(8,tdiff.getT())+chiffre(3,tdiff.getF()[1],125)*0.125f); 
}
// fazampli
if(h==30){
// sigNR[h]=0;
// ds trs13,e+fazampli modulés ensemble,
// choix de fazampli variant comme e de signr[1] à signr[2]
// floor(log10(durée=a*10^k))donne son exposant k,avec durée min=16000
// fazampli min:0.11*10a,max:durée
int expo=(int)Math.floor(Math.log10(sigNR[2]-sigNR[1]));
sigNR[h]=(int)((0.11f+(2*chiffret(8,tdiff.getT())+Math.signum(tdiff.getF()[1])*0.5f+0.5f)*0.89f/19)*(sigNR[2]-sigNR[1])*(float)Math.pow(10,chiffre(3,tdiff.getF()[1],1000/(expo+1)-expo-1))); 
} 
// typampli
if(h==31){
// sigNR[h]=1; 
sigNR[h]=chiffre(3,tdiff.getF()[1],143)+1; 
} 
// yminampli
if(h==32){
// sigNR[h]=-33000; 
sigNR[h]=sigNR[27]-sigNR[23]+Math.signum(tdiff.getF()[1])*(chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f)*2*sigNR[23];
}
// ymaxampli
if(h==33){
// sigNR[h]=33000;
// ymax=ymin+[0.1-1.0875]*2ampli
sigNR[h]=sigNR[32]+(0.1f+chiffret(8,tdiff.getT())*0.1f+chiffre(3,tdiff.getF()[1],125)*0.0125f)*2*sigNR[23]; 
}
if(h==3)sr+="\r\n"; 
SpannableString spasrbis=new SpannableString(sr);
for(int c=0;c<k;c++){
if(repR[c]!="") spasrbis.setSpan(new ForegroundColorSpan(Color.rgb(255,0,255)),sr.indexOf(repR[c]),sr.indexOf(repR[c])+30,Spanned.SPAN_EXCLUSIVE_EXCLUSIVE); 
if(repN[c]!="")spasrbis.setSpan(new ForegroundColorSpan(Color.rgb(0,200,0)),sr.indexOf(repN[c]),sr.indexOf(repN[c])+30,Spanned.SPAN_EXCLUSIVE_EXCLUSIVE); 
}
// affichage verif.params sons 
// tv[4].setText(spasrbis); 
// affichage verif.colonnes param3-30 sons
/* if(!vertical){
if(h<14){
if(h==3){
snr=""; 
for(int c=1;c<=3;c++)
tv[c].setText(snr);
}
if(h==3)snr+="h"+Integer.toString(h)+st[h]+"F"+String.format("%.2f",sigNR[h])+"\r\n";
if(h==4)snr+="h"+Integer.toString(h)+st[h]+"F"+String.format("%.2f",sigNR[h])+"\r\n"+"\r\n"; 
if(h==5||h==6) snr+="h"+Integer.toString(h)+st[3]+Integer.toString(h-3)+"F"+String.format("%.2f",sigNR[h])+"\r\n";
if(h>=7)snr+="h"+Integer.toString(h)+st[h-2]+"F"+String.format("%.2f",sigNR[h])+"\r\n";
tv[1].setText(snr);
}
if(h>=14&&h<22){
if(h==14)snr=""+"\r\n";
if(h==14)snr+="h"+Integer.toString(h)+st[h-10]+"G"+String.format("%.2f",sigNR[h])+"\r\n"+"\r\n"+"\r\n"+"\r\n"; 
if(h>=15)snr+="h"+Integer.toString(h)+st[h-10]+"G"+String.format("%.2f",sigNR[h])+"\r\n";
tv[2].setText(snr);
}
if(h>=22){
if(h==22)snr="";
if(h<=23)snr+="h"+Integer.toString(h)+st[h-19]+"A"+String.format("%.2f",sigNR[h])+"\r\n"; 
if(h==24)snr+="h"+Integer.toString(h)+"c1A"+String.format("%.2f",sigNR[h])+"\r\n";
if(h==25)snr+="h"+Integer.toString(h)+"c2A"+String.format("%.2f",sigNR[h])+"\r\n";
if(h==26)snr+="h"+Integer.toString(h)+"c3A"+String.format("%.2f",sigNR[h])+"\r\n";
if(h>=27)snr+="h"+Integer.toString(h)+st[h-22]+"A"+String.format("%.2f",sigNR[h])+"\r\n";
tv[3].setText(snr);
} 
}*/
} 
// instanpie tous les 250(Tvibr=500),alternance numpie:sa parité opposée à celle de (curtime-duret)/500,pas /250
// 250->50:augmente vitesse pie,numpie accessoire...
if((System.currentTimeMillis()-instanpie)>=50){ 
/* if(((int)(System.currentTimeMillis()-duret)/500)%2==numpie%2)
numpie=1+((int)(System.currentTimeMillis()-duret)/500)%2; 
else numpie=1+(1+(int)(System.currentTimeMillis()-duret)/500)%2; */
numpie=1;
instanpie=System.currentTimeMillis();
coordopie(); 
} 
jakasso.setpie(hauteur,largeur,numpie,xpie,ypie,anglepie,"");
// avant xpie et ypie 
// jakasso.setpie(hauteur,largeur,numpie,(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20,ypie,"");
setContentView(contenant); 
h++;
if(h==34){ 
sgen="";
sduret="";
for(int i=0;i<4;i++){
if(i==0)sgen+=Integer.toString(i)+sg[i]+Float.toString(gen[i])+"\r\n"; 
if(i==2)sgen+=Integer.toString(i)+sg[i]+String.format("%.1f",gen[i])+"\r\n";
if(i!=0&&i!=2)sgen+=Integer.toString(i)+sg[i]+String.format("%.1f",gen[i]/1000)+"\r\n"; 
} 
// affichage verif.params sons 
// String patiente=sgen+"xm"+String.format("%.1f",xminr/1000)+"\r\n"+"xM"+String.format("%.1f",xmaxr/1000)+"\r\n"+"dj"+String.format("%.1f",dj/1000)+"\r\n"+"\r\n"+
// "Veuillez"+"\r\n"+"patienter:"+"\r\n"+k+"lignes"+"\r\n"+"remplies"+"\r\n"+"sur"+gen[0];
String patiente="Veuillez"+"\r\n"+"patienter:"+"\r\n"+k+"lignes"+"\r\n"+"remplies"+"\r\n"+"sur"+gen[0];
SpannableString spatiente=new SpannableString(patiente);
spatiente.setSpan(new StyleSpan(Typeface.BOLD),0,patiente.length(),Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
tv[0].setText(spatiente); 
k++;
h=0;
if(k>gen[0]){
// float[]flaz=new float[1];
float[]flaz=(float[])laz.get(0);
// avant ypie 
// xpie=(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20;
duret=System.currentTimeMillis()-duret;
sduret=String.format("%.1f",(float)(duret)/(1000));
// affichage params
// tv[0].setText(sgen+"xm"+String.format("%.1f",xminr/1000)+"\r\n"+"xM"+String.format("%.1f",xmaxr/1000)+"\r\n"+"dj"+String.format("%.1f",dj/1000)+"\r\n"+"tm"+sduret);
plein=true;
k=0;
duret=System.currentTimeMillis();
ypie=18;
} 
}
}
else{ 
if(k>=1){
if(h==0){ 
sgen+="l.mot"+k+":"+Integer.toString((int)gen[k+1])+"\r\n";
// tv6 et 7 pour les mots 
// affichage verif.params mots
// tv[6].setText(sgen);
mot=new float[(int)gen[k+1]+4]; 
laz.add(k,mot);
// affichage verif.params mot 
// snr+="k"+Integer.toString(k)+" ";
} 
if(h==0){
if(chiffre(3,tdiff.getF()[1],143)==0)mot[h]=0.25f;
if(chiffre(3,tdiff.getF()[1],143)==1)mot[h]=0.5f;
if(chiffre(3,tdiff.getF()[1],143)==2)mot[h]=0.75f;
if(chiffre(3,tdiff.getF()[1],143)==3)mot[h]=1f;
if(chiffre(3,tdiff.getF()[1],143)==4)mot[h]=1.5f;
if(chiffre(3,tdiff.getF()[1],143)==5)mot[h]=2f;
if(chiffre(3,tdiff.getF()[1],143)==6)mot[h]=3f; 
// affichage verif.pitch 
// snr+="pi:"+String.format("%.1f",mot[h])+" ";
}
if(h==1){
if(chiffre(3,tdiff.getF()[1],125)==0)mot[h]=0.25f;
if(chiffre(3,tdiff.getF()[1],125)==1)mot[h]=0.5f;
if(chiffre(3,tdiff.getF()[1],125)==2)mot[h]=0.75f;
if(chiffre(3,tdiff.getF()[1],125)==3)mot[h]=1f;
if(chiffre(3,tdiff.getF()[1],125)==4)mot[h]=1.5f; 
if(chiffre(3,tdiff.getF()[1],125)==5)mot[h]=2f;
if(chiffre(3,tdiff.getF()[1],125)==6)mot[h]=3f;
if(chiffre(3,tdiff.getF()[1],125)==7)mot[h]=4f;
// affichage verif.rate
// snr+="ra:"+String.format("%.1f",mot[h])+" ";
}
if(h==2){ 
// modèle pause:2fois 0-500 pour 1 fois 1000 
if(chiffre(3,tdiff.getF()[1],200)==0||chiffre(3,tdiff.getF()[1],200)==1)mot[h]=0; 
if(chiffre(3,tdiff.getF()[1],200)==2||chiffre(3,tdiff.getF()[1],200)==3)mot[h]=500;
if(chiffre(3,tdiff.getF()[1],200)==4)mot[h]=1000; 
// affichage verif.pause 
// snr+="po:"+Integer.toString((int)mot[h])+" ";
}
if(h==3){
// 7 proportions voyelles-consonnes: 
// uniqt voyelles
if(chiffre(3,tdiff.getF()[1],143)==0)mot[h]=6;
// uniqt consonnes
if(chiffre(3,tdiff.getF()[1],143)==1)mot[h]=20; 
// 2*6 voyelles+1*20 consonnes 
if(chiffre(3,tdiff.getF()[1],143)==2)mot[h]=32;
// 5*6 voyelles+1*20 consonnes 
if(chiffre(3,tdiff.getF()[1],143)==3)mot[h]=50;
// 10*6voyelles+2*20 consonnes même proportion que 5*6voyelles+1*20consonnes 
// 6*6 voyelles+1*20 consonnes=56:pas possible à faire:
// chif(3,143):[0-6],2*chiffret8,500+0.5sgnt+0.5:[0-3]!=[0-7] 
// 5*6 voyelles+2*20 consonnes 
if(chiffre(3,tdiff.getF()[1],143)==4)mot[h]=70;
// 2*6 voyelles+3*20 consonnes=72: pas possible à faire,comme 56 
// 10*6 voyelles+1*20 consonnes 
if(chiffre(3,tdiff.getF()[1],143)==5)mot[h]=80;
// 10*6 voyelles+3*20 consonnes 
if(chiffre(3,tdiff.getF()[1],143)==6)mot[h]=120;
// affichage verif. proportions 
// snr+="prop."+(int)mot[h]+" ";
}
if(h>3){ 
/* modèle avec equiproba voyelle consonne
if(Math.signum(tdiff.getF()[1])>0){
// voyelles: a(97),e(101),i(105),o(111),u(117),y(121)
if(chiffre(3,tdiff.getF()[1],167)==0)mot[h]=97;
if(chiffre(3,tdiff.getF()[1],167)==1)mot[h]=101;
if(chiffre(3,tdiff.getF()[1],167)==2)mot[h]=105;
if(chiffre(3,tdiff.getF()[1],167)==3)mot[h]=111;
if(chiffre(3,tdiff.getF()[1],167)==4)mot[h]=117;
if(chiffre(3,tdiff.getF()[1],167)==5)mot[h]=121; 
}
else{
// chif(3,t,500)+2chiffret:[0-19],consonnes 0:b(98),3:f(102),6:j(106),11:p(112),16:v(118),19z(122) 
if(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())>=0 && chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())<=2)mot[h]=98+(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT()));
if(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())>=3 && chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())<=5)mot[h]=102+(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT()))%3;
if(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())>=6 && chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())<=10)mot[h]=106+(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT()))%6;
if(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())>=11 && chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())<=15)mot[h]=112+(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT()))%11;
if(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())>=16 && chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())<=18)mot[h]=118+(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT()))%16;
if(chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT())==19)mot[h]=122;
}*/
// modèle avec 7 proportions différentes(dont équiproba,c120) voyelles,consonnes:mot[3]= nfois6voyelles+p*20consonnes 
// voyelles:n fois 6: a(97),e(101),i(105),o(111),u(117),y(121)
// consonnes 6n:b(98),6n+3:f(102),6n+6:j(106),6n+11:p(112),6n+16:v(118),z(122) 
if(mot[3]==6){
// uniqt voyelles
if(chiffre(3,tdiff.getF()[1],167)==0)mot[h]=97;
if(chiffre(3,tdiff.getF()[1],167)==1)mot[h]=101;
if(chiffre(3,tdiff.getF()[1],167)==2)mot[h]=105;
if(chiffre(3,tdiff.getF()[1],167)==3)mot[h]=111;
if(chiffre(3,tdiff.getF()[1],167)==4)mot[h]=117;
if(chiffre(3,tdiff.getF()[1],167)==5)mot[h]=121;
} 
if(mot[3]==20){
// uniqt consonnes
// cvin=chif(3,t,500)+2chiffret:[0-19]
// consonnes 0:b(98),3:f(102),6:j(106),11:p(112),16:v(118),19z(122) 
int cvin=chiffre(3,tdiff.getF()[1],500)+2*chiffret(8,tdiff.getT());
if(cvin>=0 && cvin<=2)mot[h]=98+cvin;
if(cvin>=3 && cvin<=5)mot[h]=102+(cvin)%3;
if(cvin>=6 && cvin<=10)mot[h]=106+(cvin)%6;
if(cvin>=11 && cvin<=15)mot[h]=112+(cvin)%11;
if(cvin>=16 && cvin<=18)mot[h]=118+(cvin)%16;
if(cvin==19)mot[h]=122; 
} 
if(mot[3]==32){
// 2*6voyelles+1*20consonnes
// int ctrentdeu=chif(3,t,125)+8*(2chiffret/5+0.5sgnt+0.5):[0-7]+8*[0-3]=[0-31];
int c32=chiffre(3,tdiff.getF()[1],125)+8*(2*(chiffret(8,tdiff.getT())/5)+(int)(0.5f*Math.signum(tdiff.getF()[1])+0.5f));
if(c32<12){
// voyelles:2 fois 6 voyelles:a(97),e(101),i(105),o(111),u(117),y(121)
if(c32%6==0)mot[h]=97;
if(c32%6==1)mot[h]=101;
if(c32%6==2)mot[h]=105;
if(c32%6==3)mot[h]=111;
if(c32%6==4)mot[h]=117;
if(c32%6==5)mot[h]=121;
} 
else{
// consonnes 12:b(98),15:f(102),18:j(106),23:p(112),28:v(118),z(122)
if(c32>=12 && c32<=14)mot[h]=98+c32%12;
if(c32>=15 && c32<=17)mot[h]=102+(c32)%15;
if(c32>=18 && c32<=22)mot[h]=106+(c32)%18;
if(c32>=23 && c32<=27)mot[h]=112+(c32)%23;
if(c32>=28 && c32<=30)mot[h]=118+(c32)%28;
if(c32==31)mot[h]=122;
}
}
if(mot[3]==50){
// 5*6voyelles+1*20consonnes
// c50:[0-9]+10*[0-4]=[0-49]
int c50=chiffret(8,tdiff.getT())+10*chiffre(3,tdiff.getF()[1],200);
if(c50<30){
// voyelles:5 fois 6 voyelles:a(97),e(101),i(105),o(111),u(117),y(121)
if(c50%6==0)mot[h]=97;
if(c50%6==1)mot[h]=101;
if(c50%6==2)mot[h]=105;
if(c50%6==3)mot[h]=111;
if(c50%6==4)mot[h]=117;
if(c50%6==5)mot[h]=121;
}
else{
// consonnes 30:b(98),33:f(102),36:j(106),41:p(112),46:v(118),z(122) 
if(c50>=30 && c50<=32)mot[h]=98+c50%30;
if(c50>=33 && c50<=35)mot[h]=102+(c50)%33;
if(c50>=36 && c50<=40)mot[h]=106+(c50)%36;
if(c50>=41 && c50<=45)mot[h]=112+(c50)%41;
if(c50>=46 && c50<=48)mot[h]=118+(c50)%46;
if(c50==49)mot[h]=122;
}
}
if(mot[3]==70){
// 5*6voyelles+2*20consonnes
// c70:[0-9]+10*[0-6]=[0-69]
int c70=chiffret(8,tdiff.getT())+10*chiffre(3,tdiff.getF()[1],143);
if(c70<30){
// voyelles:5 fois 6 voyelles:a(97),e(101),i(105),o(111),u(117),y(121)
if(c70%6==0)mot[h]=97;
if(c70%6==1)mot[h]=101;
if(c70%6==2)mot[h]=105;
if(c70%6==3)mot[h]=111;
if(c70%6==4)mot[h]=117;
if(c70%6==5)mot[h]=121;
}
else{
// consonnes 30:b(98),33:f(102),36:j(106),41:p(112),46:v(118),49z(122) 
// consonnes 50:b(98),53:f(102),56:j(106),61:p(112),66:v(118),69z(122) 
if(c70>=30 && c70<=32)mot[h]=98+c70%30;
if(c70>=33 && c70<=35)mot[h]=102+(c70)%33;
if(c70>=36 && c70<=40)mot[h]=106+(c70)%36;
if(c70>=41 && c70<=45)mot[h]=112+(c70)%41;
if(c70>=46 && c70<=48)mot[h]=118+(c70)%46;
if(c70==49)mot[h]=122;
if(c70>=50 && c70<=52)mot[h]=98+c70%50;
if(c70>=53 && c70<=55)mot[h]=102+(c70)%53;
if(c70>=56 && c70<=60)mot[h]=106+(c70)%56;
if(c70>=61 && c70<=65)mot[h]=112+(c70)%61;
if(c70>=66 && c70<=68)mot[h]=118+(c70)%66;
if(c70==69)mot[h]=122;
}
}
if(mot[3]==80){
// 10*6voyelles+1*20consonnes
// c80:[0-9]+10*[0-7]=[0-79]
int c80=chiffret(8,tdiff.getT())+10*chiffre(3,tdiff.getF()[1],125);
if(c80<60){
// voyelles:10 fois 6 voyelles:a(97),e(101),i(105),o(111),u(117),y(121)
if(c80%6==0)mot[h]=97;
if(c80%6==1)mot[h]=101;
if(c80%6==2)mot[h]=105;
if(c80%6==3)mot[h]=111;
if(c80%6==4)mot[h]=117;
if(c80%6==5)mot[h]=121;
}
else{
// consonnes 60:b(98),63:f(102),66:j(106),71:p(112),76:v(118),79z(122) 
if(c80>=60 && c80<=62)mot[h]=98+c80%60;
if(c80>=63 && c80<=65)mot[h]=102+(c80)%63;
if(c80>=66 && c80<=70)mot[h]=106+(c80)%66;
if(c80>=71 && c80<=75)mot[h]=112+(c80)%71;
if(c80>=76 && c80<=78)mot[h]=118+(c80)%76;
if(c80==79)mot[h]=122;
}
}
if(mot[3]==120){
// 10*6voyelles+3*20consonnes
// c120:[0-9]+10*[0-11]=[0-119]
int c120=chiffret(8,tdiff.getT())+10*(2*chiffre(3,tdiff.getF()[1],167)+(int)(Math.signum(tdiff.getF()[1])*0.5f+0.5f));
if(c120<60){
// voyelles:10 fois 6 voyelles:a(97),e(101),i(105),o(111),u(117),y(121)
if(c120%6==0)mot[h]=97;
if(c120%6==1)mot[h]=101;
if(c120%6==2)mot[h]=105;
if(c120%6==3)mot[h]=111;
if(c120%6==4)mot[h]=117;
if(c120%6==5)mot[h]=121;
}
else{
if(c120>=60 && c120<=62)mot[h]=98+c120%60;
if(c120>=63 && c120<=65)mot[h]=102+(c120)%63;
if(c120>=66 && c120<=70)mot[h]=106+(c120)%66;
if(c120>=71 && c120<=75)mot[h]=112+(c120)%71;
if(c120>=76 && c120<=78)mot[h]=118+(c120)%76;
if(c120==79)mot[h]=122;
if(c120>=80 && c120<=82)mot[h]=98+c120%80;
if(c120>=83 && c120<=85)mot[h]=102+(c120)%83;
if(c120>=86 && c120<=90)mot[h]=106+(c120)%86;
if(c120>=91 && c120<=95)mot[h]=112+(c120)%91;
if(c120>=96 && c120<=98)mot[h]=118+(c120)%96;
if(c120==99)mot[h]=122;
if(c120>=100 && c120<=102)mot[h]=98+c120%100;
if(c120>=103 && c120<=105)mot[h]=102+(c120)%103;
if(c120>=106 && c120<=110)mot[h]=106+(c120)%106;
if(c120>=111 && c120<=115)mot[h]=112+(c120)%111;
if(c120>=116 && c120<=118)mot[h]=118+(c120)%116;
if(c120==119)mot[h]=122;
}
} 
snr+=Character.toString((char)((int)mot[h]));
// snr+="h"+Integer.toString(h)+" "+Float.toString(mot[h])+" ";
}
SpannableString spasnr=new SpannableString(snr);
spasnr.setSpan(new StyleSpan(Typeface.BOLD),0,snr.length(),Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
// affichage verif.colonnes mots 
// tv[7].setText(spasnr);
// instanpie tous les 250(Tvibr=500),alternance numpie:sa parité opposée à celle de (curtime-duret)/500,pas /250
// 250->50:permet d'ajuster la vitesse de la pie,numpie accessoire...
if((System.currentTimeMillis()-instanpie)>=50){ 
numpie=1;
instanpie=System.currentTimeMillis();
coordopie(); 
} 
jakasso.setpie(hauteur,largeur,numpie,xpie,ypie,anglepie,"");
// avant xpie et ypie 
// jakasso.setpie(hauteur,largeur,numpie,(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20,ypie,"");
setContentView(contenant); 
h++;
if(h>=(int)gen[k+1]+4){
String patiente="Veuillez"+"\r\n"+"patienter:"+"\r\n"+k+"mots"+"\r\n"+"remplis"+"\r\n"+"sur"+String.format("%.0f",gen[0]);
SpannableString spatiente=new SpannableString(patiente);
spatiente.setSpan(new StyleSpan(Typeface.BOLD),0,patiente.length(),Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
tv[5].setText(spatiente);
k++;
snr+="\r\n";
h=0;
}
if(k>(int)gen[0]){
// avant ypie 
// xpie=(xpie+(int)(System.currentTimeMillis()-duret)/1000)%20;
duret=System.currentTimeMillis()-duret;
sduret=String.format("%.1f",(float)(duret)/(1000));
// affichage verif. params mots 
// tv[6].setText(sgen+"tm"+sduret);
plein=true;
k=0;
duret=System.currentTimeMillis(); 
ypie=0;
}
}
}
}catch(final Throwable t){
tv[5].post(new Runnable() {
public void run() {
tv[5].setText("rempliz"+t.getMessage()+nbmots+Arrays.toString(gen)); 
}
}); 
}
}

public void dureR(float xd,float xf){
if(xd>=xminr){
if(xf>xmaxr){
if(xd>xmaxr)dj+=xd-xmaxr;
xmaxr=xf; 
}
}
else{
if(xf<=xmaxr){
if(xf<xminr)dj+=xminr-xf;
xminr=xd;
}
else{
xminr=xd;
xmaxr=xf;
}
}
}

    @Override
    protected void onPause() {     
        sensorManager.unregisterListener(this, accelerometer);
        super.onPause();
    }

    @Override
    protected void onResume() {   
        sensorManager.registerListener(this, accelerometer, SensorManager.SENSOR_DELAY_GAME);
        super.onResume();
    }

public float tronk5(float flot){
float r=-1;
float fl=Math.abs(flot); 
if((float)(Math.floor(fl*100000))/100000<fl) r=Math.signum(flot)*(float)(Math.ceil(fl*100000));
if((float)(Math.ceil(fl*100000))/100000>fl) r=Math.signum(flot)*(float)(Math.floor(fl*100000));
return r;
}
public int chiffret(int i,long t){
int d=-1;
t=t*(long)(Math.pow(10,9-Math.ceil(Math.log10(t))));
d=(int)(t/Math.pow(10,9-i))%10;
return d;
}

public int chiffre(int i,float val,int n){ 
int d=-1;
if(i==1)d=(int)Math.abs(tronk5(val))/10000;
if(i==2)d=((int)Math.abs(tronk5(val))/1000)%10;
if(i==3)d=((int)Math.abs(tronk5(val))%1000)/n; 
return d;
}

public int plusoumoins(float flot){
int d=-1;
if(flot<0)d=0;
else d=1;
return d;
}

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {       
    }

    @Override
    public void onSensorChanged(SensorEvent event) { 
try{
if (event.sensor.getType() == Sensor.TYPE_ACCELEROMETER){
n++;
if(n==0)ti=event.timestamp;  
for(int k=0;k<4;k++){
if(k==0)
listval[k].add(n,event.timestamp); 
else listval[k].add(n,event.values[k-1]);
}
if(n>0){ 
if(Math.abs((float)listval[1].get(n)-(float)listval[1].get(n-1))>=seuil
   &&Math.abs((float)listval[2].get(n)-(float)listval[2].get(n-1))>=seuil
   &&Math.abs((float)listval[3].get(n)-(float)listval[3].get(n-1))>=seuil&&plein==false){
p++;
q++;
r=0; 
for(int k=0;k<4;k++){
if(k==0){
listdiff[k].add(p,(long)listval[k].get(n)-(long)listval[k].get(n-1));
tdiff.setT(listdiff[k].get(p));
}
else{
listdiff[k].add(p,(float)listval[k].get(n)-(float)listval[k].get(n-1));
diff[k-1]=listdiff[k].get(p); 
}
} 
tdiff.setF(diff);
if(plein==false)rempliz27(tdiff); 
}
else{ 
if(q>qmax)qmax=q; 
r++;
if(r>=1){
if(r==1){
ti=event.timestamp; 
somq+=q;
nq++;
q=0; 
}
// sttuni avec paramsensor 
// sttuni="T"+Integer.toString(p+1)+" qM"+Integer.toString(qmax)+" qa"+String.format("%.1f",(float)somq/(nq))+" q"+Integer.toString(q)+" r"+Integer.toString(r)+" t"+Float.toString((float)(event.timestamp-ti)/1000000000); 
sttuni="T"+String.format("%.1f",(float)(event.timestamp-ti)/1000000000);
if(plein==false){ 
te=0;
tj=0; 
finlec=false; 
if(event.timestamp-ti>(long)(5*Math.pow(10,8))) vib.vibrate(300); 
}
else{
if(nbmots==0){
float[]genlaz=new float[4];
genlaz=(float[])laz.get(0);
if((int)genlaz[3]>0&&te>=0){
te++;
}
else{
if(tj>=0)tj++;
} 
// bool finlec à la fin de la lecture
if(finlec==true){ 
plein=false;
ti=event.timestamp; 
}
}
else{ 
if(parle==true){
parle=false; 
ti=event.timestamp; 
// langues à télécharger,une même langue par phrase
// essai fr-us-fr,3e non dit
// Exemple syntaxe:Locale langage=new Locale("ru","RU");
// langue=Locale.FRANCE; 
float[]genlaz=new float[nbmots+2];
genlaz=(float[])laz.get(0); 
texte=new String[nbmots]; 
Arrays.fill(texte,"");
pitch=new float[nbmots];
rate=new float[nbmots];
pause=new int[nbmots];
for(int k=1;k<=nbmots;k++){
float[]motlaz=new float[(int)genlaz[k]+4];
motlaz=(float[])laz.get(k);
pitch[k-1]=motlaz[0];
rate[k-1]=motlaz[1];
pause[k-1]=(int)motlaz[2];
for(int h=0;h<motlaz.length;h++){ 
if(h>=4)texte[k-1]+=Character.toString((char)((int)motlaz[h]));
}
} 
indexmot=0; 
tts=new TextToSpeech(this,this); 
}
}
}
}
} 
SpannableString spastuni=new SpannableString(""+plein+sttuni);
spastuni.setSpan(new StyleSpan(Typeface.BOLD),0,(""+plein+sttuni).length(),Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
tvl.setText(spastuni); 
if(plein==true&&nbmots>0){
if(starton==false){
// pie sautille,200 en l'air,800 au sol
if((System.currentTimeMillis()-duret)%1000<=200)jakasso.setpie(hauteur,largeur,2,(int)(xpie+(System.currentTimeMillis()-duret)/1000)%20,19,0,"");
else jakasso.setpie(hauteur,largeur,2,(int)(xpie+(System.currentTimeMillis()-duret)/1000)%20,20,0,""); 
setContentView(contenant); 
} 
}
} 
} 
}catch(Throwable t){
tv[5].setText("sensor"+t.getMessage());
}
    }
}
