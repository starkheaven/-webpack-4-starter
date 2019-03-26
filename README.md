![webpack-4-starter](https://imgur.com/XTGa3Pd.png)
# webpack-4-starter

## Особенности

* использование препроцессора [SASS](https://sass-lang.com/)
* использование транспайлера [Babel](https://babeljs.io/) для поддержки современного JavaScript (ES7) в браузерах
* использование [Webpack](https://webpack.js.org/) для сборки JavaScript-модулей


## Установка

* установите [npm](https://docs.npmjs.com/cli/install)
* скачайте сборку
* перейдите в скачанную папку со сборкой
* скачайте необходимые зависимости: ```npm install```
* чтобы начать работу, введите команду: ```npm run test``` (режим разработки)
* чтобы собрать проект, введите команду ```npm run build``` (произойдет сборка проекта, но уже итоговая (с оптимизацией, максимальной минификацией всех файлов, которую можно выкладывать на хостинг)


## Файловая структура

```
-webpack-4-starter
|
├── public                    - папка где билдится сайт
├─┬ src                       - папка с исходниками сайта
│ ├─┬ css                     - папка с css файлами
| | └── normalize.css         - файл нормализации стилей
| |
|	├── favicon                 - папка с файлами иконок
│ ├── fonts                   - папка со шрифтами
│ ├── html                    - папка заготовок HTML страниц
│ ├── img                     - папка с общими изображениями (логотип, иконки и др.)
│ ├─┬ js                      - папка с JavaScript файлами
|	|	└── postcss.config.js     - файл конфигурации postcss - процессов
| |
│ ├── sass                    - папка с SASS файлами
| ├── static                  - папка с статическими файлами для обработки
│ ├── index.html              - файл главной страницы
| └── index.js                - файл точки входа Webpack
|
├─┬ webpack_config
| ├── webpack.base.config.js
| ├── webpack.build.config.js -	 файлы конфигурации Webpack
| └── webpack.dev.config.js
|
├── package.json              - файл настроек Node.js
└── .gitignore                - запрет на отслеживание файлов Git`ом

```



## Рекомендации по использованию
* придерживайтесь изначальной структуры папок и файлов
* из всех SASS-файлов компилируется только ```main.sass```. Остальные стилевые файлы импортируются в него
* главная страница: ```src/index.html```
* шрифты находятся в папке ```src/fonts```
* изображения находятся в папке ```src/img```
* все сторонние библиотеки устанавливаются в папку ```node_modules``` с атрибутом --save (dependencies)
	* для подключения JS-файлов библиотек импортируйте их в точку входа или в JS-файл, который потом тоже импортируется. Например:
	```common.js(импортируется в index.js)

	var $ = require("jquery");

	$('#hello').html('Hello World!');
	```
	* стилевые папки библиотек подключать по тому же принципу

* в вёрстку желательно подключать только минифицированные CSS и JS-файлы. Если же файл не минифицированн тогда подключать необходимо напрямую в точку входа, ИНАЧЕ POSTCSS - процессы НА НЕМ РАБОТАТЬ НЕ БУДУТ

* Если хотите видеть изменения на всех своих устройствах одновременно в лайф режиме. Для этого в webpack.dev.config.js установлено свойство```("devServer { host: "x.x.x.x" })``` для подключения с нескольких устройств в одной локальной сети, если вы не собераетесь пользоваться подобным - можете просто его удалить. В ином случаи пропишите адрес вашего ПК в сети. Также там стоит номер порта 8081 (по умолчанию webpack слушает 8080, сделано чтобы не было конфликтов если вы юзаете что то еще)


## В сборку входит 
	*	webpack 4
	* babel 7
	* препроцессор SASS
	* postcss-плагины:
		* autoprefixer - раставляет префиксы
		* css-mqpacker - сжимает медиа запросы
		* cssnano 		 - максимально минифицирует исходные стили
	* magic-css      - готовый набор анимаций для взаимодействия с jquery   
	* jquery библиотека
	* file-loader, copy-webpack-plugin (обработчик изображений)
	* html-webpack-plugin

## ВАЖНО
	* в конфигурационном файле ```webpack.base.config.js``` прописан обьект ```PATHS``` со всеми путями, соответственно для изменения названий папок и прочего при билде проекта, достаточно сделать это там и все. Остальные пути автоматически изменятся.

## Сборка создана для личного пользования и предназначена для автоматизации задач в повседневной front-end разработке.

## Также конфигурация вебпака разделена на 3 файла, чтобы при дев-разработке не подключать обработчики изоюражений и т.д
