# Тестовое задание: react native

## Общая суть
В `React Native`-проект будет необходимо установить определенную `React Native`-библиотеку и доработать ее код некоторым образом (все подробности смотрите в разделах [Порядок выполнения задания](#порядок-выполнения-задания) и [Дополнительная информация](#дополнительная-информация)).

## Порядок выполнения задания

### 1. Создайте `React Native`-проект на версии `0.68.5`
### 2. Установите библиотеку `react-native-ussd-dial` с помощью `yarn` или `npm`

Yarn:

```sh
yarn add react-native-ussd-dial
```

npm:

```sh
npm install --save react-native-ussd-dial
```
### 3. Доработайте код данной библиотеки таким образом, чтобы:
* Проект корректно собирался и запускался на обеих платформах, `Android` и `iOS`
* В коде какого-нибудь `.js`-файла (например, `App.js`) корректно работала следующая логика:
  ```js
  // импортируем установленную библиотеку
  import RNUssdDial from 'react-native-ussd-dial';

  const App = () => {
    
    // функция getDeviceName, которая вызывает интересующий метод библиотеки
    const getDeviceName = async () => {
      // метод библиотеки должен с помощью `async-await` возвращать из нативного кода (Java, Obj-C) строковое значение модели девайса
      const deviceName = await RNUssdDial.getDeviceName();
      // выводим в консоль полученное значение модели девайса
      console.log('deviceName: ', deviceName);
    };

    return (
      // рендерим кнопку
      <Button
        onPress={getDeviceName} // при нажатии на кнопку происходит вызов функции getDeviceName
        title="get device name"
        color="#841584"
      />
    );
  };
  ```

## Дополнительная информация
### Работа с кодом
* Изменения, которые будут внесены в код библиотеки `react-native-ussd-dial`, необходимо добавить в код вашего проекта в виде patch'а с помощью библиотеки [patch-package](https://www.npmjs.com/package/patch-package).
* Сам проект можно будет залить на `github` и скинуть ссылку на репозиторий либо скинуть в виде архива.

### Работа с библиотекой `react-native-ussd-dial`:
* библиотека имеет свой [github-репозиторий](https://github.com/Kwamena-S/react-native-ussd-dial), однако код [библиотеки на сайте npmjs.com](https://www.npmjs.com/package/react-native-ussd-dial) не соответствует коду библиотеки в репозитории, поэтому необходимо работать именно с кодом библиотеки, установленной через `yarn` или `npm`
* при изучении кода библиотеки можно увидеть, что модель девайса на `Android`'е получается на основе значения `android.os.Build.MODEL`, а на `iOS` метод получения модели девайса вообще не реализрован. Поэтому для получения модели девайса на `iOS` необходимо взять код, находящийся внутри метода [getDeviceId, библиотека react-native-device-info](https://github.com/react-native-device-info/react-native-device-info/blob/master/ios/RNDeviceInfo/RNDeviceInfo.m#L386-L395)