2кт запросы 



GET - pm.test("1.Статут ответа 200 OK",function(){
    pm.response.to.have.status(200);
});
pm.test("2.Content-Type is present",function(){
    pm.response.to.have.header("Content-Type")
})
pm.test("3.Проверка скорости работы Java",function(){
    pm.expect(pm.response.responseTime).to.be.below(1000); // 1 секунда
});
pm.test("4.Проверка чтобы список вернулся в виде массива", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.be.an('array');
});

pm.test("5.Проверка что в списке есть хоть 1 книга", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.length).to.be.above(0);
});
pm.test("6.Проверка id первой книги равна настоящему id книги ",function(){
    var jsonData=pm.response.json();
    pm.expect(jsonData[0].id).to.be.eql("6a29a7c050934d309e06edb3");
});

pm.test("7.Проверка является ли author строкой", function() {
    var jsonData = pm.response.json();

    pm.expect(jsonData[0].author).to.be.a('string');
});
pm.test("8.Проверка является ли author строкой", function() {
    var jsonData = pm.response.json();

    pm.expect(jsonData[0].author).to.be.a('string');
});
pm.test("9.роверка, что у первой книги год публикации ЗАПОЛНЕН firstpublisher",function(){
    var jsonData=pm.response.json();
    pm.expect(jsonData[0].firstPublishYear).to.not.be.null;
});

pm.test("10.Проверка что хоть где то в спике есть заполненное поле firstPublishYear",function(){
    var jsonData=pm.response.json();
    pm.expect(jsonData.some(book => book.firstPublishYear !== null)).to.be.true;

});

pm.test("11.Проверка что книг 9", function (){
        var jsonData=pm.response.json();
    pm.expect(jsonData.length).to.equal(9);
});


pm.test("12.Проверка что первая книга - 'Война и мир'", function () {
        var jsonData=pm.response.json();
    pm.expect(jsonData[0].title).to.equal('Война и мир ');
});


DELETE-// Проверяем, что сервер успешно обработал удаление (код 200 или 204)
pm.test("Книга успешно удалена", function () {
    pm.expect(pm.response.code).to.be.oneOf([200, 204]);
});
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


POST-pm.test("Сервер успешно ответил", function () {
    pm.expect(pm.response.code).to.be.oneOf([200, 201]);
});
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
