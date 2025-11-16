Oczywiście! Poniżej znajdziesz prosty przykładowy test w JavaScript z wykorzystaniem Selenium WebDriver. Ten test otwiera stronę Google, wyszukuje hasło „Selenium” i sprawdza, czy tytuł strony zawiera słowo „Selenium”.

```javascript
const { Builder, By, Key, until } = require('selenium-webdriver');

(async function exampleTest() {
  // Uruchamiamy przeglądarkę Chrome
  let driver = await new Builder().forBrowser('chrome').build();

  try {
    // Przechodzimy na stronę Google
    await driver.get('https://www.google.com');

    // Znajdujemy pole wyszukiwania, wpisujemy "Selenium" i zatwierdzamy Enterem
    await driver.findElement(By.name('q')).sendKeys('Selenium', Key.RETURN);

    // Czekamy, aż tytuł strony zacznie się słowem "Selenium"
    await driver.wait(until.titleContains('Selenium'), 5000);

    // Pobieramy tytuł strony i wypisujemy go
    let title = await driver.getTitle();
    console.log(`Tytuł strony to: ${title}`);

    if (title.toLowerCase().includes('selenium')) {
      console.log('Test passed: Tytuł zawiera słowo "Selenium".');
    } else {
      console.log('Test failed: Tytuł nie zawiera słowa "Selenium".');
    }

  } catch (error) {
    console.error('Wystąpił błąd:', error);
  } finally {
    // Zamykamy przeglądarkę
    await driver.quit();
  }
})();
```

Aby uruchomić ten test, pamiętaj o:

- Zainstalowaniu `selenium-webdriver` (`npm install selenium-webdriver`)
- Posiadaniu odpowiedniego WebDrivera (np. chromedriver) zgodnego z Twoją przeglądarką Chrome i dostępnym w PATH.