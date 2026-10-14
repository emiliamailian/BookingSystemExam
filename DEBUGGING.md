FELSÖKNINGSRAPPORT:

Felet med överlappande bokningar, som jag arbetade med när jag skulle få funktionen för att skapa bokningar att fungera.



Jag började med att köra de färdiga tester i Test Explorer. Jag startade också programmet och testade att skapa bokningar själv för att förstå hur det fungerade. Sen gick jag tillbaka till koden och försökte hitta varför vissa tester inte gick igenom.



När jag arbetade med Create() i BookingService.cs behövde jag bland annat kontrollera att två bokningar inte kunde överlappa varandra. Jag gick igenom metoden Validate() och jämförde den med vad testerna förväntade sig.



Ett av testerna utgick från en befintlig bokning mellan 09:00 och 11:00 och försökte skapa en ny bokning mellan 08:00 och 10:00. De bokningarna överlappar ju varandra, men den gamla kontrollen kunde ändå godkänna den nya bokningen. Resultatet skulle istället ha varit att bokningen nekades med ett meddelande om att rummet redan var bokat under den tiden.



När jag tittade närmare på villkoret förstod jag att problemet var hur tiderna jämfördes. Koden kontrollerade bara om den nya bokningens starttid låg inom den befintliga bokningen. Om den nya bokningen började tidigare än den befintliga missades överlappningen eftersom starttiden låg utanför den befintliga bokningens intervall.



Jag ändrade därför villkoret till:



booking.StartTime < existing.EndTime \&\&

booking.EndTime > existing.StartTime



Som jag förstår det betyder det att den nya bokningen måste börja innan den befintliga slutar och sluta efter att den befintliga börjar för att tiderna ska överlappa. Det gör att kontrollen fungerar även när en bokning börjar tidigare än den andra.



Efter ändringen körde jag testerna igen i Test Explorer. Testet Create\_WhenBookingOverlapsExistingBooking\_ReturnsFailure blev grönt. Det testar fyra olika tidsintervall och hjälper till att upptäcka om samma fel skulle komma tillbaka. Jag kontrollerade också testet Create\_WhenBookingStartsWhenExistingBookingEnds\_ReturnsSuccess, eftersom två bokningar ska kunna ligga direkt efter varandra utan att räknas som överlappande.



Jag har försökt använda mig utav testerna flitigt, både för att lättare få perspektiv men också förståelse i hur man vill att programmet ska bete sig, också för att förstå vad som var fel och kontrollera mina ändringar. Det jag tar med mig från felsökningen är att försöka förstå varför ett villkor inte fungerar, istället för att bara ändra kod tills testet blir grönt.

