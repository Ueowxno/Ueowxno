#29



HTML Code

The HTML code to validate a credit card and find out what type of credit card it is is shown below.




<form action="" method="POST">

Credit card number:<input type="text" name="number_entered" value='<?php if ($submitbutton) { echo "$number";} ?>'/> 
<?php 
if ($submitbutton)
{
if (validatecard($number) !== false)
{
echo "<green> $type detected. credit card number is valid</green>";
}
else
{
echo " <red>This credit card number is invalid</red>";
}
}
?>

<br><br>

<input type="submit" value="Submit" name="submitbutton"/>

</form>






So the above code is the HTML needed to create the form to enter a credit card number. You can see that it also has PHP code inside of it.

So the first thing we do is create a form. Since we want to keep the data posted to this page, we set the action attribute equal to "" and the method attribute equal to POST. Therefore, the form posts data to the current page.

We then create a credit card text box. Since we want the text box to retain the value that a user enters, we set the value attribute equal to the $number. You'll see later that this $number holds the credit card number that the user entered. We put PHP code by the right side of this text box. This PHP code checks a function called validatecard to see whether the card is valid or not. This will update right next to the credit card box when a user presses Submit.

We then code the Submit button and end the form.

PHP Code

The PHP code that validates a credit card is shown below.



<?php

$submitbutton= $_POST['submitbutton'];

$number= $_POST['number_entered'];

function validatecard($number)
 {
    global $type;

    $cardtype = array(
        "visa"       => "/^4[0-9]{12}(?:[0-9]{3})?$/",
        "mastercard" => "/^5[1-5][0-9]{14}$/",
        "amex"       => "/^3[47][0-9]{13}$/",
        "discover"   => "/^6(?:011|5[0-9]{2})[0-9]{12}$/",
    );

    if (preg_match($cardtype['visa'],$number))
    {
	$type= "visa";
        return 'visa';
	
    }
    else if (preg_match($cardtype['mastercard'],$number))
    {
	$type= "mastercard";
        return 'mastercard';
    }
    else if (preg_match($cardtype['amex'],$number))
    {
	$type= "amex";
        return 'amex';
	
    }
    else if (preg_match($cardtype['discover'],$number))
    {
	$type= "discover";
        return 'discover';
    }
    else
    {
        return false;
    } 
 }

validatecard($number);


?>






So we retrieve the submit button data, so that we can know whether it has been clicked or not. We store this in the variable $submitbutton.

We retrieve the credit card number that the user has entered into the text box and store it in the variable $number.

We then create a function called validatecard and have it have a $number parameter.

We then create a global variable named $type.

We then create an array named $cardtype. This array holds a series of major credit companies. We use regular expressions to determine which credit card number belongs to which major credit card company based on the beginning numbers of the credit card.

Visa credit card numbers begin with 4. Visa credit cards can either be composed of 13 digits or 16 numbers. Older visa cards contained 13 digits. Newer visa cards now have 16 digits.

Mastercard credit card numbers begin with 5. Mastercards are composed of 16 digits.

American express cards start with either 34 or 37. Amex cards are composed of 15 digits.

Discover cards begin with 6. Discover cards are composed of either 13 or 16 digits.

If you understand regular expressions, these are what are encoded in the PHP code.

Once we have these regular expressions coded in the various credit card types, we'll be able to know whether or not they are valid based on whether the number the user enters matches the regular expressions.

To see if they match, we use the PHP preg_match function, comparing the element in the array (each various credit card type) to the number that the user enters. The preg_match() function takes 2 parameters. The first is the element in the array we created. And this array represents each card type we specified. The 2nd parameter is the number that the user enters into the text box. If the number is a match, fitting the regular expression, we return the credit card. In each if statement, we had the variable $type and set it equal to the credit card type it is.

Else, if there are no matches, we return false.

We then simply call the function validatecard so that we actually execute it.

If you go back to the HTML code above right next to the text box, where the user enters his or her credit card number, we have PHP code.

We run an if statement to see if what the function returns is not equal to false. If not equal to false (if it is true), we output the card detected and that the credit card number is valid.

If what the function returns is equal to false, then we output that the credit card number is invalid.

And this is all that is required to validate a credit card using PHP.

Of course, there is so much more advanced analytics involved in this. We have taken into account expiration dates and the security code. That requires much more advanced analytics, in which you basically have to contact the credit card vendor to get confirmation. And this is normally what when the actual payment is submitted. You would then have to check the actual vendor. But what we are doing here is simply checking the format and seeing whether is card value initially just by the numbers that the user enters. If the credit card number isn't valued, then we're going to waste resources, sending this number to the credit card vendor to be processed when it's erroneous to begin with. It first has to be in correct format. This doesn't mean that the actual credit card is correct, but the format is. It's the right number of digits, beginning with the right numbers. Then after that, we can send the information to a credit card to be processed. But before we do that, we first have to make sure the credit card number to begin with. So this is what we're doing.

