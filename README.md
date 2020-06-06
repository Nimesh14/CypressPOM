# CypressPOM
This repository has code snippet for POM design pattern using Cypress


Page Object Model (POM) is a design pattern, popularly used in test automation that creates Object Repository for web UI elements. 
Advantage :
The advantage of the model is that it reduces code duplication and improves test maintenance

How to create a POM in Cypress	

Follow 2 steps :
1. Create a folder named page_objects under Cypress folder and add the individual pages as class  files under page_objects folder.
2. Create a folder under Cypress>integration folder and add  an end to end functionality class file under the same folder which should     extend the class files of the individual pages we want to cover as part of end to end flow.


-------->Basic architecture of individual page class files

/// <reference types="cypress" />
class BasePage {
    launchApplication(){
     cy.visit("https://parabank.parasoft.com/parabank/index.htm")
    }
    logOutFromApplication(){
     cy.contains('Log Out').click()
    }
}
export default BasePage  //Here export keyword stands for inheritance principle

-------->Basic architecture of End to End test

/// <reference types="cypress" />
import LoginPage from "../../page_objects/LoginPage"
import BillPaymentsPage from "../../page_objects/BillPaymentsPage"
import BasePage from "../../page_objects/BasePage"
 
const loginPage = new LoginPage
const billPaymentsPage = new BillPaymentsPage
const basePage = new BasePage
 
describe("Bill Payment Test",()=>{
    it("Pay a Bill",()=>{
        loginPage.login()
        billPaymentsPage.enterPayeeDetailsAndPay("Nimesh","UK","London","Dummy","09860236456","12345","12345","12345","13011","100")
        basePage.logOutFromApplication()
    })
})

