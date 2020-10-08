# 📅 ion5-schedule

- Soporte de rango de fechas.
- Soporte de múltiples fechas.
- Soporte de componentes HTML.
- Desactivar días laborables o fines de semana.
- Evento de días de configuración.
- Configuración de localización.

# Soporte

- @ionic/angular `^5.0.0`

# Uso

### Instalación

`$ npm install ion5-schedule moment --save`

### Importación de Módulos

```typescript
import { NgModule } from '@angular/core';
import { IonicApp, IonicModule } from '@ionic/angular';
import { MyApp } from './app.component';
...
import { CalendarModule } from 'ion5-schedule';

@NgModule({
  declarations: [
    MyApp,
    ...
  ],
  imports: [
    IonicModule.forRoot(),
    CalendarModule
  ],
  bootstrap: [MyApp],
  ...
})
export class AppModule {}
```

### Cambiar valores predeterminados

```typescript
import { NgModule } from '@angular/core';
import { IonicApp, IonicModule } from 'ionic-angular';
import { MyApp } from './app.component';
...
import { CalendarModule } from "ion2-calendar";

@NgModule({
  declarations: [
    MyApp,
    ...
  ],
  imports: [
    IonicModule.forRoot(MyApp),
    // Consulte CalendarComponentOptions para conocer las opciones.
    CalendarModule.forRoot({
      doneLabel: 'Save',
      closeIcon: true
    })
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    ...
  ]
})
export class AppModule {}
```

# Modo de componentes

### Básico

```html
<ion-calendar [(ngModel)]="date"
              (change)="onChange($event)"
              [type]="type"
              [format]="'YYYY-MM-DD'">
</ion-calendar>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
  date: string;
  type: 'string'; // 'string' | 'js-date' | 'moment' | 'time' | 'object'
  constructor() { }

  onChange($event) {
    console.log($event);
  }
  ...
}
```

### Rango de fechas

```html
<ion-calendar [(ngModel)]="dateRange"
              [options]="optionsRange"
              [type]="type"
              [format]="'YYYY-MM-DD'">
</ion-calendar>
```

```typescript
import { Component } from '@angular/core';
import { CalendarComponentOptions } from 'ion2-calendar';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
  dateRange: { from: string; to: string; };
  type: 'string'; // 'string' | 'js-date' | 'moment' | 'time' | 'object'
  optionsRange: CalendarComponentOptions = {
    pickMode: 'range'
  };

  constructor() { }
  ...
}
```

### Fecha múltiple

```html
<ion-calendar [(ngModel)]="dateMulti"
              [options]="optionsMulti"
              [type]="type"
              [format]="'YYYY-MM-DD'">
</ion-calendar>
```

```typescript
import { Component } from '@angular/core';
import { CalendarComponentOptions } from 'ion2-calendar';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
  dateMulti: string[];
  type: 'string'; // 'string' | 'js-date' | 'moment' | 'time' | 'object'
  optionsMulti: CalendarComponentOptions = {
    pickMode: 'multi'
  };

  constructor() { }
  ...
}
```

### Propiedades de entrada

| Nombre   | Tipo                     | Defecto      | Descripción  |
| -------- | ------------------------ | ------------ | ------------ |
| options  | CalendarComponentOptions | null         | options      |
| format   | string                   | 'YYYY-MM-DD' | value format |
| type     | string                   | 'string'     | value type   |
| readonly | boolean                  | false        | readonly     |

### Propiedades de salida

| Nombre      | Tipo         | Descripción                      |
| ----------- | ------------ | ------------------------------------------------- |
| change      | EventEmitter | evento para cambio de modelo                      |
| monthChange | EventEmitter | evento por cambio de mes                          |
| select      | EventEmitter | evento para hacer clic en el botón del día        |
| selectStart | EventEmitter | evento para hacer clic en el botón del día        |
| selectEnd   | EventEmitter | evento para hacer clic en el botón del día        |

### CalendarComponentOptions

| Nombre            | Tipo                    | Default                                                                                | Descripción                                       |
| ----------------- | ----------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------- |
| from              | Date                    | `new Date()`                                                                           | start date                                        |
| to                | Date                    | 0 (Infinite)                                                                           | end date                                          |
| color             | string                  | `'primary'`                                                                            | 'primary', 'secondary', 'danger', 'light', 'dark' |
| pickMode          | string                  | `single`                                                                               | 'multi', 'range', 'single'                        |
| showToggleButtons | boolean                 | `true`                                                                                 | show toggle buttons                               |
| showMonthPicker   | boolean                 | `true`                                                                                 | show month picker                                 |
| monthPickerFormat | Array<string>           | `['ENE', 'FEB', 'MAR', 'ABR', 'MAY', 'JUN', 'JUL', 'AGO', 'SEP', 'OCT', 'NOV', 'DIC']` | month picker format                               |
| defaultTitle      | string                  | ''                                                                                     | default title in days                             |
| defaultSubtitle   | string                  | ''                                                                                     | default subtitle in days                          |
| disableWeeks      | Array<number>           | `[]`                                                                                   | week to be disabled (0-6)                         |
| monthFormat       | string                  | `'MMM YYYY'`                                                                           | month title format                                |
| weekdays          | Array<string>           | `['SA', 'LU', 'MA', 'MI', 'JU', 'VI', 'DO']`                                                  | weeks text                                        |
| weekStart         | number                  | `0` (0 or 1)                                                                           | set week start day                                |
| daysConfig        | Array<**_DaysConfig_**> | `[]`                                                                                   | days configuration                                |

# Modo modal

### Básico

Importe ion5-schedule en el controlador del componente.

```typescript
import { Component } from '@angular/core';
import { ModalController } from '@ionic/angular';
import {
  CalendarModal,
  CalendarModalOptions,
  DayConfig,
  CalendarResult
} from 'ion5-schedule';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {
  constructor(public modalCtrl: ModalController) {}

  openCalendar() {
    const options: CalendarModalOptions = {
      title: 'BASIC'
    };

    const myCalendar = await this.modalCtrl.create({
      component: CalendarModal,
      componentProps: { options }
    });

    myCalendar.present();

    const event: any = await myCalendar.onDidDismiss();
    const date: CalendarResult = event.data;
    console.log(date);
  }
}
```

### Date range

Establezca pickMode en 'range'.

```typescript
openCalendar() {
  const options: CalendarModalOptions = {
    pickMode: 'range',
    title: 'RANGE'
  };

  const myCalendar = await this.modalCtrl.create({
    component: CalendarModal,
    componentProps: { options }
  });

  myCalendar.present();

  const event: any = await myCalendar.onDidDismiss();
  const date = event.data;
  const from: CalendarResult = date.from;
  const to: CalendarResult = date.to;

  console.log(date, from, to);
}
```

### Multi Date

Set pickMode to 'multi'.

```typescript
openCalendar() {
  const options = {
    pickMode: 'multi',
    title: 'MULTI'
  };

  const myCalendar = await this.modalCtrl.create({
    component: CalendarModal,
    componentProps: { options }
  });

  myCalendar.present();

  const event: any = await myCalendar.onDidDismiss();
  const date: CalendarResult = event.data;
  console.log(date);
}
```

### Desactivar semanas

Utilice el índice, por ejemplo: `[0, 6]` denota domingo y sábado.

```typescript
openCalendar() {
  const options: CalendarModalOptions = {
    disableWeeks: [0, 6]
  };

  const myCalendar = await this.modalCtrl.create({
    component: CalendarModal,
    componentProps: { options }
  });

  myCalendar.present();

  const event: any = await myCalendar.onDidDismiss();
  const date: CalendarResult = event.data;
  console.log(date);
}
```

### Localización

your root module

```typescript
import { NgModule, LOCALE_ID } from '@angular/core';
...

@NgModule({
  ...
  providers: [{ provide: LOCALE_ID, useValue: "zh-CN" }]
})

...
```

```typescript
openCalendar() {
  const options: CalendarModalOptions = {
    monthFormat: 'YYYY 年 MM 月 ',
    weekdays: ['天', '一', '二', '三', '四', '五', '六'],
    weekStart: 1,
    defaultDate: new Date()
  };

  const myCalendar = await this.modalCtrl.create({
    component: CalendarModal,
    componentProps: { options }
  });

  myCalendar.present();

  const event: any = await myCalendar.onDidDismiss();
  const date: CalendarResult = event.data;
  console.log(date);
}
```

### Configuración de días

Configurar un día.

```typescript
openCalendar() {
  let _daysConfig: DayConfig[] = [];
  for (let i = 0; i < 31; i++) {
    _daysConfig.push({
      date: new Date(2017, 0, i + 1),
      subTitle: `$${i + 1}`
    })
  }

  const options: CalendarModalOptions = {
    from: new Date(2017, 0, 1),
    to: new Date(2017, 11.1),
    daysConfig: _daysConfig
  };

  const myCalendar = await this.modalCtrl.create({
    component: CalendarModal,
    componentProps: { options }
  });

  myCalendar.present();

  const event: any = await myCalendar.onDidDismiss();
  const date: CalendarResult = event.data;
  console.log(date);
}
```

# API

### Opciones del modo modal

| Nombre                    | Tipo                     | Defecto                               | Description                                                |
| ------------------------- | ------------------------ | ------------------------------------- | ---------------------------------------------------------- |
| from                      | Date                     | `new Date()`                          | start date                                                 |
| to                        | Date                     | 0 (Infinite)                          | end date                                                   |
| title                     | string                   | `'CALENDAR'`                          | title                                                      |
| color                     | string                   | `'primary'`                           | 'primary', 'secondary', 'danger', 'light', 'dark'          |
| defaultScrollTo           | Date                     | none                                  | let the view scroll to the default date                    |
| defaultDate               | Date                     | none                                  | default date data, apply to single                         |
| defaultDates              | Array<Date>              | none                                  | default dates data, apply to multi                         |
| defaultDateRange          | { from: Date, to: Date } | none                                  | default date-range data, apply to range                    |
| defaultTitle              | string                   | ''                                    | default title in days                                      |
| defaultSubtitle           | string                   | ''                                    | default subtitle in days                                   |
| cssClass                  | string                   | `''`                                  | Additional classes for custom styles, separated by spaces. |
| canBackwardsSelected      | boolean                  | `false`                               | can backwards selected                                     |
| pickMode                  | string                   | `single`                              | 'multi', 'range', 'single'                                 |
| disableWeeks              | Array<number>            | `[]`                                  | week to be disabled (0-6)                                  |
| closeLabel                | string                   | `CANCEL`                              | cancel button label                                        |
| doneLabel                 | string                   | `DONE`                                | done button label                                          |
| clearLabel                | string                   |  null                                 | clear button label                                         |
| closeIcon                 | boolean                  | `false`                               | show cancel button icon                                    |
| doneIcon                  | boolean                  | `false`                               | show done button icon                                      |
| monthFormat               | string                   | `'MMM YYYY'`                          | month title format                                         |
| weekdays                  | Array<string>            | `['S', 'M', 'T', 'W', 'T', 'F', 'S']` | weeks text                                                 |
| weekStart                 | number                   | `0` (0 or 1)                          | set week start day                                         |
| daysConfig                | Array<**_DaysConfig_**>  | `[]`                                  | days configuration                                         |
| step                      | number                   | `12`                                  | month load stepping interval to when scroll                |
| defaultEndDateToStartDate | boolean                  | `false`                               | makes the end date optional, will default it to the start  |

### onDidDismiss Output `{ data } = event`

| pickMode | Tipo                                                     |
| -------- | -------------------------------------------------------- |
| single   | { date: **_CalendarResult_** }                           |
| range    | { from: **_CalendarResult_**, to: **_CalendarResult_** } |
| multi    | Array<**_CalendarResult_**>                              |

### onDidDismiss Output `{ role } = event`

| Value      | Description                          |
| ---------- | ------------------------------------ |
| 'cancel'   | dismissed by click the cancel button |
| 'done'     | dismissed by click the done button   |
| 'backdrop' | dismissed by click the backdrop      |

#### DaysConfig

| Nombre   | Tipo    | Defecto  | Descripción                                     |
| -------- | ------- | -------- | ----------------------------------------------- |
| cssClass | string  | `''`     | separados por espacios                          |
| date     | Date    | required | días configurados                               |
| marked   | boolean | false    | resaltar el color                               |
| disable  | boolean | false    | inhabilitar                                     |
| title    | string  | none     | título mostrado, por ejemplo: `'today'`         |
| subTitle | string  | none     | subtítulo mostrado, por ejemplo: `'New Year\'s'`|

### CalendarResult

| Nombre  | Tipo   |
| ------- | ------ |
| time    | number |
| unix    | number |
| dateObj | Date   |
| string  | string |
| years   | number |
| months  | number |
| date    | number |

## Gracias por leer

