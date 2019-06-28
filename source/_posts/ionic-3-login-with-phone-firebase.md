---
title: ionic 3 - login with phone firebase
date: 2019-03-19 16:14:13
tags:
---

### Activate Authentication Provider in Console

Authentication -> Sign-in method

Then set Phone enabled


### install angularfire2

https://github.com/angular/angularfire2/blob/master/docs/ionic/v3.md

$ npm install angularfire2 firebase promise-polyfill --save
<!-- more -->


### Add Firebase to your web app


{% codeblock app.module.ts %}

import * as firebase from 'firebase/app';
import { AngularFireModule } from '@angular/fire';
import { AngularFireAuthModule } from '@angular/fire/auth';

export const firebaseConfig = {
  apiKey: "AIzaSyDIg_uDHWGJra-R952amrCwo9IJJHiWmUA",
  authDomain: "visitor-clinic.firebaseapp.com",
  databaseURL: "https://visitor-clinic.firebaseio.com",
  projectId: "visitor-clinic",
  storageBucket: "visitor-clinic.appspot.com",
  messagingSenderId: "789622100904"
};

firebase.initializeApp(firebaseConfig);


...
imports: [
BrowserModule,
IonicModule.forRoot(MyApp),
AngularFireModule.initializeApp(firebaseConfig),
AngularFireAuthModule
],
...

{% endcodeblock %}



ionic g page loginphone


{% codeblock loginphone.html %}

<ion-header>
  <ion-navbar>
    <ion-title>Masuk</ion-title>
  </ion-navbar>
</ion-header>

<ion-content padding>
  <ion-item>
    <ion-label stacked>Nomor Ponsel</ion-label>
    <ion-input type="number" placeholder="Contoh: 62852433xxxxx" [(ngModel)]="phoneNumber"></ion-input>
  </ion-item>
  <div id="recaptcha-container"></div>
</ion-content>

<ion-footer>
  <button ion-button full large color="dark" (click)="signIn(phoneNumber)">
      Masuk
  </button>
</ion-footer> 

{% endcodeblock %}


{% codeblock loginphone.ts %}

import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams, AlertController, ToastController } from 'ionic-angular';
import * as firebase from 'firebase/app';

@IonicPage()
@Component({
  selector: 'page-loginphone',
  templateUrl: 'loginphone.html',
})
export class LoginphonePage {

  public recaptchaVerifier:firebase.auth.RecaptchaVerifier;

  constructor(public navCtrl: NavController,
    private toastController: ToastController,
    public navParams: NavParams, 
    public alertCtrl: AlertController) {
  }

  ionViewDidLoad() {
    this.recaptchaVerifier = new firebase.auth.RecaptchaVerifier('recaptcha-container');
  }

  signIn(phoneNumber: number){
    const appVerifier = this.recaptchaVerifier;
    const phoneNumberString = "+" + phoneNumber;

    if(phoneNumber){

      firebase.auth().signInWithPhoneNumber(phoneNumberString, appVerifier)
        .then( confirmationResult => {
          // SMS sent. Prompt user to type the code from the message, then sign the
          // user in with confirmationResult.confirm(code).
          let prompt = this.alertCtrl.create({
          title: 'Kode konfirmasi',
          inputs: [{ name: 'confirmationCode', placeholder: '6 digit kode' }],
          buttons: [
            { text: 'Batal',
              handler: data => { console.log('Cancel clicked'); }
            },
            { text: 'Konfirmasi',
              handler: data => {
                confirmationResult.confirm(data.confirmationCode)
                  .then(result =>{
                    // User signed in successfully.
                    if(result){
                      this.navCtrl.setRoot('ProduksPage');
                    }

                  }).catch(error => {
                    // User couldn't sign in (bad verification code?)
                    if(error){
                      this.presentToast('Kode verifikasi tidak cocok.')
                    }
                    // ...
                  });
              }
            }
          ]
        });
        prompt.present();
      })
      .catch(err => {        
        if(err){
          this.presentToast('Nomor ponsel yang Anda masukkan tidak sesuai.');
        }
      })
      // .catch(function (error) {
      //   console.error("SMS not sent", error.message);
      // });
      

    }else{
      this.presentToast('Masukkan nomor ponsel Anda.');
    }

  }

  presentAlert(tit, sub) {
    let alert = this.alertCtrl.create({
      title: tit,
      subTitle: sub,
      buttons: ['Ok']
    });
    alert.present();
  }
  
  presentToast(msg) {
    let toast = this.toastController.create({
      message: msg,
      position: 'bottom',
      duration: 3000
    });
    toast.onDidDismiss(() => {
      // console.log('Dismissed toast');
    });
    toast.present();
  }

}

{% endcodeblock %}


{% codeblock app.module.ts%}
delete HomePage

  declarations: [
    MyApp
  ],

{% endcodeblock %}