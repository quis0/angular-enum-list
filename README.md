# angular-enum-list

This package can be used for transformation enum's values to array where names are your own path with namespace and dictionary name to localizate word.



 - [Installation](#installation)
 - [Usage](#usage)
 - [Dictionary](#dictionary)
 
 
# Installation

**1.** Install package
    npm install angular-enum-list --save
    

**2.** Import AngularEnumListModule to AppModule

```typescript

import { AngularEnumListModule } from 'angular-enum-list';

@NgModule({
  bootstrap: [ AppComponent ],
  declarations: [   
    AppComponent
  ],
  import: [
    AngularEnumListModule.forRoot('enums') // first parameter is localization namespace name,
                                           // second parameter is separator, default ':'
  ]
})
export class AppModule {}

```

You can configurate name of localize namespase for global context and separator which break namespace and path from localize key



# Usage

### Pipes

Use "enumList" pipe to get the array with translation keys:

    <div *ngFor="let item of myEnum | enumList: { dictName: 'list' }" [id]="item.id">{{ item.name | i18next }}</div>
    
Pipe has one required parameter "dictName". It's name of dictionary in localization file.
Other params are optional. You can add the folowing parametrs:

```canBeEmpty```
```<div *ngFor="let item of myEnum | enumList: { dictName: 'list', canBeEmpty: true }" [id]="item.id">
 {{ item.name | i18next }}
</div>```

If in your enum is "Undefined" field, will be ignored this one.

```nameSpace```

```<div *ngFor="let item of myEnum | enumList: { dictName: 'list', nameSpace: 'my-favorite-enums' }" [id]="item.id">
 {{ item.name | i18next }}
</div>```

You can specify nameSpace parameter for particularly pipes.

# Dictionary

Your own dictionary must be looks like:

ru.enums.json
```
{
"SexKind": {
    "Undefined": "Не выбрано"
    "Male": "Мужской",
    "Female": "Женский"
  }
}
 ```
 
 You can use this list in native select in html-file:

```<select class="form-control"
            formControlName="SexKind"
            [(ngModel)]="model.SexKind"
            validationMessage>
      <option *ngFor='let status of _enums.SexKind | enumList : { canBeEmpty: false, dictName: "SexKind" }'
              [ngValue]='status.id'>
        {{ status.name | i18nextCap }}
      </option>
    </select>
    ```

in this code ```_enums``` is public variable which contains enums you need in your template:

```public _enums = { SexKind, RaceKind };```
