# ionic2-pincode-input

[![Dependency Status](https://david-dm.org/HsuanXyz/ionic2-pincode-input.svg)](https://david-dm.org/HsuanXyz/ionic2-pincode-input)
[![NPM version][npm-image]][npm-url] [![Downloads][downloads-image]][downloads-url] [![MIT License][license-image]][license-url]

A pin-code input for ionic2

[中文文档](https://github.com/HsuanXyz/ionic2-pincode-input/blob/master/README-CN.md)

![v](https://github.com/HsuanXyz/hsuanxyz.github.io/blob/master/assets/ionic2-pincode-input/pin-code.gif?raw=true)



## install

`npm install ionic2-pincode-input --save`

## use

app.module.ts
```typescript
import { NgModule, ErrorHandler } from '@angular/core';
import { IonicApp, IonicModule, IonicErrorHandler } from 'ionic-angular';
import { MyApp } from './app.component';
...

import { PincodeInputModule } from  'ionic2-pincode-input';

@NgModule({
  declarations: [
    MyApp,
    ...
  ],
  imports: [
    PincodeInputModule,
    IonicModule.forRoot(MyApp),
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    ...
  ],
  providers: [{provide: ErrorHandler, useClass: IonicErrorHandler}]
})
export class AppModule {}
```
your-page.ts

```typescript
import { Component } from '@angular/core';

import { NavController } from 'ionic-angular';
import { PincodeController } from  'ionic2-pincode-input/dist/pincode'
@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  code:string;

  constructor(
    public navCtrl: NavController,
    public pincodeCtrl: PincodeController,
  ) {
  }

  openPinCode():any{

    let pinCode =  this.pincodeCtrl.create({
      title:'Pincode'
    });

    pinCode.present();

    pinCode.onDidDismiss( (code,status) => {

      if(status === 'done'){

        this.code = code;
      }else if (status === 'forgot'){

        // forgot password
      }

    })

  }

}

```


## create(PincodeOpt)

### PincodeOpt
| Name            | Type          | Default       | Description |
| --------------- | ------------- | ------------- | ----------- |
| title           | String        | `'password'`  | title       |
| cancelButtonText| String        | `'cancel'`    | cancel button text    |
| encoded         | Function      | ` (c) => {return c} ` | your encoded pin code function |
| forgotPasswordText| String      | `'forgot password'`| forgot password text    |
| hideForgotPassword| Boolean     | `false`       | is hide forgot password button   |
| enableBackdropDismiss| Boolean     | `true`       | Whether the alert should be dismissed by tapping the backdrop.  |

[npm-url]: https://www.npmjs.com/package/ionic2-pincode-input
[npm-image]: https://img.shields.io/npm/v/ionic2-pincode-input.svg

[downloads-image]: https://img.shields.io/npm/dm/ionic2-pincode-input.svg
[downloads-url]: http://badge.fury.io/js/ionic2-pincode-input

[license-image]: http://img.shields.io/badge/license-MIT-blue.svg?style=flat
[license-url]: LICENSE
