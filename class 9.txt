let countries;

fetch('https://restcountries.com/v3.1/all')
    .then((res) => res.json())
    .then((data) => {
        initialize(data);

        region();
        population();
        details();
        totalPopulation();
        currency();

    })
    .catch((err) => console.log(err));


function initialize(data) {

    countries = data;
}

function region() {

    countries.filter((ele) => ele.region == "Asia")
        .map((ele) => ele.name.common).forEach(ele => console.log(ele));

}

function population() {
    console.log('countries with a population of less than 2 lakhs');
    countries.filter((ele) => ele.population < 200000)
        .map((ele) => ele.name.common).forEach(ele => console.log(ele));
}

function details() {
    countries.forEach(element => {
        console.log(
            `Name : ${element.name.common}
Capital : ${element.capital}
flag : ${element.flag}`
        )
    });
}

function totalPopulation() {
    console.log('total population',
        countries.reduce((total, ele) => total + ele.population, 0)
    );
}

function currency() {
    console.log('Print the country which uses US Dollars as currency.');
    console.log(Object.keys(countries[0].currencies)[0] == "AFN");
    console.log(countries.filter((ele) => {
        if (ele.hasOwnProperty('currencies'))
            return Object.keys(ele.currencies)[0] == "USD"
        return false;
    }));
}