
![java regular expression tutorials](http://www.mkyong.com/wp-content/uploads/2010/04/regular-expression-tutorials.png)

Java has comprehensive support for Regular Expression functionality through the **java.util.regex** package. The regular expression language is easy to learn but hard to master, the better way to learn it is through examples. In theoretical, regular expression can match almost any stuff you want, the only limitation is in your imagination.

Happy learning Java Regular Expression :)

*   [Username regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-username-with-regular-expression/)  
    Username regular expression example in Java and unit tested with TestNG.

        ^[a-z0-9_-]{3,15}$

*   [Password regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-password-with-regular-expression/)  
    Password regular expression example in Java and unit tested with TestNG.

        ((?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%]).{6,20})

*   [Hex color code regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-hex-color-code-with-regular-expression/)  
    Hex color code regular expression example in Java and unit tested with TestNG.

        ^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$

*   [E-mail address regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-email-address-with-regular-expression/)  
    E-mail address regular expression example in Java and unit tested with TestNG.

        ^[_A-Za-z0-9-]+(\\.[_A-Za-z0-9-]+)*@
        [A-Za-z0-9]+(\\.[A-Za-z0-9]+)*(\\.[A-Za-z]{2,})$

*   [Image file extension regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-image-file-extension-with-regular-expression/)  
    Image file extension regular expression example in Java and unit tested with TestNG.

        ([^\s]+(\.(?i)(jpg|png|gif|bmp))$)

*   [IP Address regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-ip-address-with-regular-expression/)  
    IP Address regular expression example in Java and unit tested with TestNG.

        ^([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\.([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\.
        ([01]?\\d\\d?|2[0-4]\\d|25[0-5])\\.([01]?\\d\\d?|2[0-4]\\d|25[0-5])$

*   [Time in 12 Hours format regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-time-in-12-hours-format-with-regular-expression/)  
    Time in 12 Hours format regular expression example in Java and unit tested with TestNG.

        (1[012]|[1-9]):[0-5][0-9](\\s)?(?i)(am|pm)

*   [Time in 24 Hours format regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-time-in-24-hours-format-with-regular-expression/)  
    Time in 24 Hours format regular expression example in Java and unit tested with TestNG.

        ([01]?[0-9]|2[0-3]):[0-5][0-9]

*   [Date regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-date-with-regular-expression/)  
    Date regular expression example in Java and unit tested with TestNG.

        (0?[1-9]|[12][0-9]|3[01])/(0?[1-9]|1[012])/((19|20)\\d\\d)

*   [HTML tag regular expression](http://www.mkyong.com/regular-expressions/how-to-validate-html-tag-with-regular-expression/)  
    HTML tag regular expression example in Java and unit tested with TestNG.

        <("[^"]*"|'[^']*'|[^'">])*>

*   [HTML Links regular expression](http://www.mkyong.com/regular-expressions/how-to-extract-html-links-with-regular-expression/)  
    HTML links regular expression example in Java and unit tested with TestNG.

        (?i)<a([^>]+)>(.+?)</a>

        \s*(?i)href\s*=\s*(\"([^"]*\")|'[^']*'|([^'">\s]+));

## Reference

*   [Wiki Regular Expression](http://en.wikipedia.org/wiki/Regular_expression)
*   [Java Regular Expression lesson from SUN (Oracle)](http://java.sun.com/docs/books/tutorial/essential/regex/index.html)
*   [Another Regular Expression lession](http://www.regular-expressions.info/java.html)
