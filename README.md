Создайте фуллстек-приложение с рецептами блюд, которое будет использовать Django Rest Framework, автодокументацию OpenAPI+Swagger и react-router.

Давать пользователю возможность создавать рецепты не нужно: достаточно распределить их по категориям и отображать в клиенте и в API.

Где отображать документацию API — решать вам.

У каждого блюда и каждой категории должна быть своя страница: с главной страницы можно перейти на любую из категорий, а из категории — на любой рецепт этой категории.

Загрузить проект:

окрываем новый проект в IDE

в терминале git clone https://github.com/albinadesign/F4-Recipes.git

cd F4-New

python3 -m venv venv или python -m venv venv (1 - для Mac, 2 - для Windows)

source venv/bin/activate

cd recipes

pip install -r requirements.txt

Запустить в одном терминале: python manage.py runserver

и в другом терминале:

cd F4-New/recipes/frontend

npm i

npm start

Запускается проект по адресу http://localhost:3000/ 

![image](https://github.com/albinadesign/F4-New/assets/117900508/23934795-6212-4cc3-9dc9-71aae2d69666)


Можно выбрать категорию 

![image](https://github.com/albinadesign/F4-New/assets/117900508/9130b65f-e48e-4365-ae1f-a7ef9e712ca4)


Переходим на страницу категории 

![image](https://github.com/albinadesign/F4-New/assets/117900508/6f3160ab-746d-4034-afe2-41cbd6792cdb)


Щелкаем на рецепт, переходим на страницу рецепта 

![image](https://github.com/albinadesign/F4-New/assets/117900508/52947969-7585-4d78-91a0-42c8d832654c)


Оттуда же можно вернуться на главную страницу или посмотреть все рецепты данной категории

![image](https://github.com/albinadesign/F4-New/assets/117900508/9f4ebdb3-b98f-4282-9500-9fd2c8f2c3bf)


Теперь API:

Вносить новые рецепты и менять старые может только admin

По адресу http://localhost:8000/api/swagger/ видим Swagger

![image](https://github.com/albinadesign/F4-New/assets/117900508/d060f4c0-b12f-43ee-a382-466dd0849e6d)


![image](https://github.com/albinadesign/F4-New/assets/117900508/8a55e687-9f97-4308-acec-32ae087fe29f)



По ссылке http://localhost:8000/api/swagger.json скачивается файл документации:

swagger: '2.0' info: title: Recipe API description: Recipe API description license: name: My License version: v1 host: localhost:8000 schemes:

http basePath: /api consumes:
application/json produces:
application/json securityDefinitions: Basic: type: basic security:
Basic: [] paths: /categories/: get: operationId: categories_list description: '' parameters: [] responses: '200': description: '' schema: type: array items: $ref: '#/definitions/Category' tags: - categories post: operationId: categories_create description: '' parameters: - name: data in: body required: true schema: $ref: '#/definitions/Category' responses: '201': description: '' schema: $ref: '#/definitions/Category' tags: - categories parameters: [] /categories/{id}/: get: operationId: categories_read description: '' parameters: [] responses: '200': description: '' schema: $ref: '#/definitions/Category' tags: - categories put: operationId: categories_update description: '' parameters: - name: data in: body required: true schema: $ref: '#/definitions/Category' responses: '200': description: '' schema: $ref: '#/definitions/Category' tags: - categories patch: operationId: categories_partial_update description: '' parameters: - name: data in: body required: true schema: $ref: '#/definitions/Category' responses: '200': description: '' schema: $ref: '#/definitions/Category' tags: - categories delete: operationId: categories_delete description: '' parameters: [] responses: '204': description: '' tags: - categories parameters:
name: id in: path description: A unique integer value identifying this category. required: true type: integer /recipes-by-category/: get: operationId: recipes-by-category_list description: '' parameters:
name: category_id in: query description: category_id required: false type: string responses: '200': description: '' schema: type: array items: $ref: '#/definitions/Recipe' tags:
recipes-by-category parameters: [] /recipes/: get: operationId: recipes_list description: '' parameters: [] responses: '200': description: '' schema: type: array items: $ref: '#/definitions/Recipe' tags:
recipes post: operationId: recipes_create description: '' parameters:
name: data in: body required: true schema: $ref: '#/definitions/Recipe' responses: '201': description: '' schema: $ref: '#/definitions/Recipe' tags:
recipes parameters: [] /recipes/{id}/: get: operationId: recipes_read description: '' parameters: [] responses: '200': description: '' schema: $ref: '#/definitions/Recipe' tags:
recipes put: operationId: recipes_update description: '' parameters:
name: data in: body required: true schema: $ref: '#/definitions/Recipe' responses: '200': description: '' schema: $ref: '#/definitions/Recipe' tags:
recipes patch: operationId: recipes_partial_update description: '' parameters:
name: data in: body required: true schema: $ref: '#/definitions/Recipe' responses: '200': description: '' schema: $ref: '#/definitions/Recipe' tags:
recipes delete: operationId: recipes_delete description: '' parameters: [] responses: '204': description: '' tags:
recipes parameters:
name: id in: path description: A unique integer value identifying this recipe. required: true type: integer definitions: Category: required:
name type: object properties: id: title: ID type: integer readOnly: true name: title: Name type: string maxLength: 50 minLength: 1 Recipe: required:
category
title
description type: object properties: id: title: ID type: integer readOnly: true category: $ref: '#/definitions/Category' title: title: Title type: string maxLength: 100 minLength: 1 description: title: Description type: string minLength: 1 image: title: Image type: string readOnly: true format: uri
