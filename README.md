# **Postman** (Collections and work environment)

# HW_1

Создать запросы в Postman.

Protocol: `http`
IP: `162.55.220.72`
Port: `5005`

EP_1
Method: `GET`
EndPoint: `/get_method`
request url params: 
 `name: str
 age: int`

response: 
`[
   “Str”,
   “Str”
]`

==================

EP_2
Method: `POST`
EndPoint: `/user_info_3`
request form data: 
 `name: str
 age: int
 salary: int`

response: 
`{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'u_salary_1_5_year': salary * 4}
 }`


==================

EP_3
Method: `GET`
EndPoint: `/object_info_1`
request url params: 
 `name: str
 age: int
 weight: int`

response: 
`{'name': name,
          'age': age,
          'daily_food': weight * 0.012,
          'daily_sleep': weight * 2.5}`


==================

EP_4
Method: `GET`
EndPoint: `/object_info_2`
request url params: 
 `name: str
 age: int
 salary: int`

response: 
`{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
 }`


==================

EP_5
Method: `GET`
EndPoint: `/object_info_3`
request url params: 
 `name: str
 age: int
 salary: int`

response: 
`{'name': name,
          'age': age,
          'salary': salary,
          'family': {'children': [['Alex', 24], ['Kate', 12]],
                     'pets': {'cat':{'name':'Sunny',
                                     'age': 3},
                              'dog':{'name':'Luky',
                                     'age': 4}},
                     'u_salary_1_5_year': salary * 4}
}`


==================

EP_6
Method: `GET`
EndPoint: `/object_info_4`
request url params: 
 `name: str
 age: int
 salary: int`

response: 
`{'name': name,
          'age': int(age),
          'salary': [salary, str(salary * 2), str(salary * 3)]}`


==================

EP_7
Method: `POST`
EndPoint: `/user_info_2`
request form data: 
`name: str
 age: int
 salary: int`

response: 
`{'start_qa_salary': salary,
          'qa_salary_after_6_months': salary * 2,
          'qa_salary_after_12_months': salary * 2.7,
          'qa_salary_after_1.5_year': salary * 3.3,
          'qa_salary_after_3.5_years': salary * 3.8,
          'person': {'u_name': [user_name, salary, age],
                     'u_age': age,
                     'u_salary_5_years': salary * 4.2}
          }`
          
# HW_2

http://162.55.220.72:5005/first
1. Отправить запрос.
2. Статус код 200
3. Проверить, что в body приходит правильный string.

`pm.test("Body is correct", function () {
    pm.response.to.have.body('This is the first responce from server!ss');
});

pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("This is the first responce from server!ss");
});`

http://162.55.220.72:5005/user_info_3
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Проверить, что name в ответе равно name s request (name вбить руками.)
5. Проверить, что age в ответе равно age s request (age вбить руками.)
6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
7. Спарсить request.
8. Проверить, что name в ответе равно name s request (name забрать из request.)
9. Проверить, что age в ответе равно age s request (age забрать из request.)
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
11. Вывести в консоль параметр family из response.
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)

`let resp_data = pm.response.json();
let req_data = request.data

pm.test("Check name response", function () {
        pm.expect(resp_data.name).to.eql('Jess');
});

pm.test("Check age response", function () {
        pm.expect(resp_data.age).to.eql('33');
});

pm.test("Check salary response", function () {
        pm.expect(resp_data.salary).to.eql(1000);
});


pm.test("Check name response", function () {
        pm.expect(resp_data.name).to.eql(req_data.name);
});

pm.test("Check age response", function () {
        pm.expect(resp_data.age).to.eql(req_data.age);
});

pm.test("Check salary response", function () {
        pm.expect(resp_data.salary).to.eql(+req_data.salary);
});

console.log(resp_data.family)

let req_slary = +req_data.salary
let resp_salary_1_5_years = resp_data.family.u_salary_1_5_year

pm.test("Check u_salary_1_5_year", function () {
        pm.expect(req_data.salary*4).to.eql(resp_salary_1_5_years);
});`


http://162.55.220.72:5005/object_info_3
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age s request (age забрать из request.)
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
8. Вывести в консоль параметр family из response.
9. Проверить, что у параметра dog есть параметры name.
10. Проверить, что у параметра dog есть параметры age.
11. Проверить, что параметр name имеет значение Luky.
12. Проверить, что параметр age имеет значение 4.

`let resp_data = pm.response.json();
let req_data = pm.request.url.query.toObject()

pm.test("Check name response", function () {
        pm.expect(resp_data.name).to.eql(req_data.name);
});

pm.test("Check age response", function () {
        pm.expect(resp_data.age).to.eql(req_data.age);
});

pm.test("Check salary response", function () {
        pm.expect(resp_data.salary).to.eql(+req_data.salary);
});

console.log(resp_data.family)

pm.test("Check name_type", function () {
        pm.expect(resp_data.name).to.be.a('String');
});


pm.test("Check all properties", function () {
        pm.expect(resp_data).to.have.keys("age", "family", "name", "salary");
});

pm.test("Check inner properties", function () {
        pm.expect(resp_data.family).to.have.any.keys("children", "u_salary_1_5_year");
});

pm.test("Check dog_name properties", function () {
        pm.expect(resp_data.family.pets.dog).to.have.any.keys("name");
});

pm.test("Check dog_age properties", function () {
        pm.expect(resp_data.family.pets.dog).to.have.any.keys("age");
});

pm.test("Check dog_name_Luky response", function () {
        pm.expect(resp_data.family.pets.dog.name).to.eql("Luky");
});

pm.test("Check dog_age_4 response", function () {
        pm.expect(resp_data.family.pets.dog.age).to.eql(4);
});`

http://162.55.220.72:5005/object_info_4
1. Отправить запрос.
2. Статус код 200
3. Спарсить response body в json.
4. Спарсить request.
5. Проверить, что name в ответе равно name s request (name забрать из request.)
6. Проверить, что age в ответе равно age из request (age забрать из request.)
7. Вывести в консоль параметр salary из request.
8. Вывести в консоль параметр salary из response.
9. Вывести в консоль 0-й элемент параметра salary из response.
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
15. Создать в окружении переменную name
16. Создать в окружении переменную age
17. Создать в окружении переменную salary
18. Передать в окружение переменную name
19. Передать в окружение переменную age
20. Передать в окружение переменную salary
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.

`let resp_data = pm.response.json();
let req_data = pm.request.url.query.toObject()

pm.test("Check name response", function () {
        pm.expect(resp_data.name).to.eql(req_data.name);
});

pm.test("Check age response", function () {
        pm.expect(resp_data.age).to.eql(+req_data.age);
});

console.log(req_data.salary)
console.log(resp_data.salary)
console.log(resp_data.salary[0])
console.log(+resp_data.salary[1])
console.log(+resp_data.salary[2])

pm.test("Check salary_0 response", function () {
        pm.expect(resp_data.salary[0]).to.eql(+req_data.salary);
});

pm.test("Check salary_1 response", function () {
        pm.expect(+resp_data.salary[1]).to.eql(+req_data.salary*2);
});

pm.test("Check salary_2 response", function () {
        pm.expect(+resp_data.salary[2]).to.eql(+req_data.salary*3);
});

var_name = resp_data.name
var_age = resp_data.age
var_salary = req_data.salary

console.log("---- " + var_salary)

pm.environment.set("name", var_name)
pm.environment.set("age", var_age)
pm.environment.set("salary", var_salary)

// for (let i = 0; i < resp_data.salary.leght; i++) {
//     console.log(resp_data.salary[i])
// }

for (item in resp_data.salary) {
    console.log("I == " + resp_data.salary[item])
}`

http://162.55.220.72:5005/user_info_2
1. Вставить параметр salary из окружения в request
2. Вставить параметр age из окружения в age
3. Вставить параметр name из окружения в name
4. Отправить запрос.
5. Статус код 200
6. Спарсить response body в json.
7. Спарсить request.
8. Проверить, что json response имеет параметр start_qa_salary
9. Проверить, что json response имеет параметр qa_salary_after_6_months
10. Проверить, что json response имеет параметр qa_salary_after_12_months
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
13. Проверить, что json response имеет параметр person
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.

`let resp_data = pm.response.json();
let req_data = request.data

pm.test("Check qa_salary_after_1.5_year", function () {
        pm.expect(resp_data).to.have.property("qa_salary_after_1.5_year")
});

pm.test("Check qa_salary_after_12_months", function () {
        pm.expect(resp_data).to.have.property("qa_salary_after_12_months")
});

pm.test("Check qa_salary_after_3.5_years", function () {
        pm.expect(resp_data).to.have.property("qa_salary_after_3.5_years")
});

pm.test("Check qa_salary_after_6_months", function () {
        pm.expect(resp_data).to.have.property("qa_salary_after_6_months")
});

pm.test("Check start_qa_salary", function () {
        pm.expect(resp_data).to.have.property("start_qa_salary")
});

pm.test("Check start_qa_salary = request", function () {
        pm.expect(resp_data.start_qa_salary).to.eql(+req_data.salary);
});

pm.test("Check qa_salary_after_6_months = salary*2", function () {
        pm.expect(resp_data.qa_salary_after_6_months).to.eql(+req_data.salary*2);
});

pm.test("Check qa_salary_after_12_months = salary*2.7", function () {
        pm.expect(resp_data.qa_salary_after_12_months).to.eql(+req_data.salary*2.7);
});

pm.test("Check qa_salary_after_1.5_year = salary*3.3", function () {
        pm.expect(resp_data["qa_salary_after_1.5_year"]).to.eql(+req_data.salary*3.3);
});

pm.test("Check qa_salary_after_3.5_years = salary*3.8", function () {
        pm.expect(resp_data["qa_salary_after_3.5_years"]).to.eql(+req_data.salary*3.8);
});

pm.test("Check u_name[1] = salary_request", function () {
        pm.expect(resp_data.person.u_name[1]).to.eql(+req_data.salary);
});

pm.test("Check u_age = age_request", function () {
        pm.expect(resp_data.person.u_age).to.eql(+req_data.age);
});

pm.test("Check u_salary_5_years = salary*4.2", function () {
        pm.expect(resp_data.person.u_salary_5_years).to.eql(+req_data.salary*4.2);
});

// for (let = 0; i < resp_data.person.u_name.length; i++) {
//     console.log(resp_data.person.u_name[i])
// }

for (item in resp_data.person.u_name) {
    console.log("I == " + resp_data.person.u_name[item])
}`
