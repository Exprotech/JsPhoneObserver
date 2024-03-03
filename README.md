# JsPhoneObserver
JsPhoneObserver is a JavaScript project implementing a telephone class with an observer pattern.
// Define a generic Observer class with an empty update method
class Observer {
  update(phoneNumber) {}
}

// Define a specific observer for logging dialed phone numbers
class PhoneNumberObserver extends Observer {
  update(phoneNumber) {
    console.log(`Phone number dialed: ${phoneNumber}`);
  }
}

// Define another observer for logging custom dialing messages
class CustomMessageObserver extends Observer {
  update(phoneNumber) {
    console.log(`Now Dialing ${phoneNumber}`);
  }
}

// Define the Telephone class
class Telephone {
  // Constructor to initialize phone numbers and observers
  constructor() {
    this.phoneNumbers = new Set(); // Use a Set to store unique phone numbers
    this.observers = []; // An array to store registered observers
  }

  // Method to add an observer to the list
  addObserver(observer) {
    this.observers.push(observer);
  }

  // Method to remove an observer from the list
  removeObserver(observer) {
    const index = this.observers.indexOf(observer);
    if (index !== -1) {
      this.observers.splice(index, 1);
    }
  }

  // Method to notify all observers when a phone number is dialed
  notifyObservers(phoneNumber) {
    this.observers.forEach((observer) => {
      observer.update(phoneNumber);
    });
  }

  // Method to add a phone number to the list
  addPhoneNumber(phoneNumber) {
    this.phoneNumbers.add(phoneNumber);
  }

  // Method to remove a phone number from the list
  removePhoneNumber(phoneNumber) {
    this.phoneNumbers.delete(phoneNumber);
  }

  // Method to dial a phone number and notify observers
  dialPhoneNumber(phoneNumber) {
    if (this.phoneNumbers.has(phoneNumber)) {
      console.log(`Dialing ${phoneNumber}`);
      this.notifyObservers(phoneNumber);
    } else {
      console.log(`Error: Phone number ${phoneNumber} not found.`);
    }
  }
}

// Example usage:

// Creating instances of observers
const phoneNumberObserver = new PhoneNumberObserver();
const customMessageObserver = new CustomMessageObserver();

// Creating an instance of the telephone
const telephone = new Telephone();

// Adding observers to the telephone
telephone.addObserver(phoneNumberObserver);
telephone.addObserver(customMessageObserver);

// Adding phone numbers
telephone.addPhoneNumber("1234567890");
telephone.addPhoneNumber("2345678901");

// Dialing a phone number
telephone.dialPhoneNumber("1234567890");
telephone.dialPhoneNumber("2345678901");  // This will trigger both observers


## Explanation:

## Class Definitions:
 The code defines three classes - Observer, PhoneNumberObserver, and CustomMessageObserver.
## Constructor: 
 The Telephone class has a constructor that initializes phone numbers and observers using Set and an array.
## Methods:
 Methods are defined for adding/removing observers, notifying observers, adding/removing phone numbers, and dialing phone numbers.
## Observer Pattern:
 The observers are notified when a phone number is dialed, allowing for different actions to be taken based on the observers attached.
## Example Usage: 
The code demonstrates how to create instances of observers, add them to the telephone, add phone numbers, and dial phone numbers, triggering observer notifications.