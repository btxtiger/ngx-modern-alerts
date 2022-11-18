# ngx-modern-alerts

[![npm](https://img.shields.io/npm/v/ngx-modern-alerts.svg)](https://www.npmjs.com/package/ngx-modern-alerts)
[![npm](https://img.shields.io/npm/dm/ngx-modern-alerts.svg)](https://www.npmjs.com/package/ngx-modern-alerts)
[![npm](https://img.shields.io/librariesio/release/npm/ngx-modern-alerts)](https://www.npmjs.com/package/ngx-modern-alerts)

### Advanced modern customizable alerts for Angular

```sh
# Install the Angular component
npm i -S ngx-modern-alerts
```

### <a href="https://btxtiger.github.io/ngx-modern-alerts/" target="_blank">⇨ DEMO</a>

### Show global alerts using the service

```ts
@NgModule({
   imports: [BrowserAnimationsModule],
   providers: [NgxModernAlertService],
})
export class AppModule {}
```

```ts
import { NgxModernAlert } from "ngx-modern-alerts";
import { timeout } from "rxjs";

export class AppComponent {
   constructor(private modernAlertService: NgxModernAlertService) {
   }

   /**
    * Show Floating Alerts
    */
   public showFloatingAlerts(): void {
      this.modernAlertService.alertInfo('Information!');
      this.modernAlertService.alertSuccess('Success!');
      this.modernAlertService.alertWarning('Warning!');
      this.modernAlertService.alertDanger('Danger!');
   }

   /**
    * Show Banner Alerts
    */
   public showBannerAlerts(): void {
      this.modernAlertService.alertBannerInfo('Information!');
      this.modernAlertService.alertBannerSuccess('Success!');
      this.modernAlertService.alertBannerWarning('Warning!');
      this.modernAlertService.alertBannerDanger('Danger!');
   }

   /**
    * Show Custom Alert
    */
   public showCustomAlert(): void {
      const alert = new NgxModernAlert();
      alert.message = 'This is my message!';
      alert.level = 'success';
      alert.svgIcon = this.customSvgIcon;
      alert.validUntil = moment().add(10, 'seconds').toDate();
      alert.overlayType = 'floating';

      this.modernAlertService.showAlert(alert);

      timeout(5000).subscribe(() => {
         this.modernAlertService.dismissAlert(alert);
      });
   }

}
```

### Using the component
You can also render the component in classic form in your template:
```ts
@NgModule({
   imports: [NgxModernAlertsModule],
})
export class AppModule {}
```

```html
<ngx-modern-alert [text]="text" level="danger" (dismiss)="onDismissed()"></ngx-modern-alert>

// Hide icon
<ngx-modern-alert [text]="text" level="info" [hideIcon]="true"></ngx-modern-alert>

// Use alert object
<ngx-modern-alert [alert]="alert" [hideIcon]="true"></ngx-modern-alert>
```

### Styling

You can modify these variables to adjust the style, and e.g. add compatibility to your dark mode.

```scss
.ngx-modern-alert {
   --ngx-modern-alert-bg-default: rgb(255 255 255 / 80%);
   --ngx-modern-alert-text-default: rgb(30 30 30);

   --ngx-modern-alert-info-color-icon: #2196f3;
   --ngx-modern-alert-info-color-text: hsl(220, 50%, 35%);

   --ngx-modern-alert-success-color-icon: #4caf50;
   --ngx-modern-alert-success-color-text: hsl(125, 50%, 35%);

   --ngx-modern-alert-danger-color-icon: #f44336;
   --ngx-modern-alert-danger-color-text: hsl(0, 50%, 35%);

   --ngx-modern-alert-warning-color-icon: #ea9c00;
   --ngx-modern-alert-warning-color-text: hsl(25, 50%, 35%);
}

body.dark {
   .ngx-modern-alert {
      --ngx-modern-alert-bg-default: rgb(30 30 30 / 85%);
      --ngx-modern-alert-text-default: rgb(200 200 200);
      
      --ngx-modern-alert-info-color-icon: #2196f3;
      --ngx-modern-alert-info-color-text: hsl(220, 50%, 65%);
      
      --ngx-modern-alert-success-color-icon: #4caf50;
      --ngx-modern-alert-success-color-text: hsl(125, 50%, 65%);
      
      --ngx-modern-alert-danger-color-icon: #f44336;
      --ngx-modern-alert-danger-color-text: hsl(0deg 50% 65%);
      
      --ngx-modern-alert-warning-color-icon: #ea9c00;
      --ngx-modern-alert-warning-color-text: hsl(25, 50%, 65%);
   }
}
```