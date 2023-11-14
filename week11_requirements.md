# Software Engineering Week11 submission Project work 4

## The Task

Week 10 is the third and last week in a series in which the goal is to improve your 
personal software engineering practice. Your portfolio entry has the same general content
as last week's, including:

* A descriptive summary of the issue that you worked on.
* Snippets from your code with commentary showing how you have used good software design 
  practice.
* A descriptive summary of the test code that you have written.
* A reflective summary of any changes that were requested during the code review along 
  with your fixes.
* A descriptive summary of any issues you found with the code that you were asked to review.
* A general reflective section that identifies, for example,
  * New things you have realised this week
  * Common problems that can arise in a team development situation
  * How your practice compares to other people's
  * etc.

Be sure to include links to the original items in the team's GitHub repository.

In the reflective sections this week, you should highlight ways that you persona practice
has improved as before. It would also be good to reflect on any improvements that have
been made to the agreed team workflow and related procedures. Are things working
better than they were? What further improvements could be made in the future?

## The Issue number 89
As an UNDAC Deputy Team Leader I want to view overall status of operational sub-teams
so that I can identify and resolve issues as they arise.

## The code
```csharp
//This contains methods to handle user interactions on the View Security Alerts Page.


using System.Collections.ObjectModel;
using UNDAC_App.Classes;
using UNDAC_App.Models;

namespace UNDAC_App;

public partial class ViewSecurityAlertsPage : ContentPage
{
    private ObservableCollection<SecurityAlert> securityAlerts; //! Collection of security alert objects
    private readonly SecurityAlertDB securityAlertDB; //! Instance of the security alerts database table manager class
    public ObservableCollection<SecurityAlert> SecurityAlerts { get => securityAlerts; set => securityAlerts = value; } //! Getter and setter for the collection of alerts

    public ViewSecurityAlertsPage() //! Default constructor of the class
	{
		InitializeComponent();

        securityAlertDB = new SecurityAlertDB(); //! Instantiate the security alert database table manager
        SecurityAlerts = new ObservableCollection<SecurityAlert>(securityAlertDB.ReadSecurityAlerts()); //! Read all the security alerts from the database into a collection

        SecurityAlertsListview.ItemsSource = SecurityAlerts; //! Set the listview item source to the observable collection
    }

    private void RefreshSecurityAlertsList() //! A method that will update the list of security alerts in the user interface.
    {
        SecurityAlerts.Clear(); //! Clear the collection of security alerts
        foreach (SecurityAlert alert in securityAlertDB.ReadSecurityAlerts()) //! Iterate through all the stored security alerts
        {
            SecurityAlerts.Add(alert); //! Add the security alert to the collection
        }
    }



    private async void CreateNewSecurityAlert(object sender, EventArgs e) //! A method that will create a new security alert.
    {
        SecurityAlert newAlert = new(); //! Create an empty alert
        string newSecurityAlertTitle = await DisplayPromptAsync("Create Security Alert", "Enter the new Security Alert:"); //! Prompt the user for input

        if (!string.IsNullOrWhiteSpace(newSecurityAlertTitle)) //! Validate the entry
        {
            newAlert.ChangeSecurityAlertName(newSecurityAlertTitle); //! Change the name of the alert
            securityAlertDB.CreateSecurityAlert(newAlert); //! Create the alert in the database
            RefreshSecurityAlertsList(); //! Refresh the UI
        }
    }

    // Event handlers for editing a security alert

    // When alert is tapped
    private async void SelectSecurityAlert(object sender, ItemTappedEventArgs e) //! An event handler for when a security alert in the list is tapped.
    {
        if (e.Item is SecurityAlert alert) //! If the item that was tapped is a security alert
        {
            string updatedAlert = await DisplayPromptAsync("Edit Security Alert", "Edit the Security Alert:", initialValue: alert.AlertTitle); //! Prompt the user for input

            if (!string.IsNullOrWhiteSpace(updatedAlert))
            {
                alert.ChangeSecurityAlertName(updatedAlert);    //! Change the title of the alert
                securityAlertDB.EditSecurityAlert(alert);       //! Pass the editied alert to be u[pdated in the database table
                RefreshSecurityAlertsList();                    //! Refresh the list of items in the user interface.
            }
        }
    }

    // Event handler when alert is edited
    private async void EditSecurityAlert(object sender, EventArgs e) //! An event handler for when a security alert in the list is clicked.
    {
        Button button = sender as Button;

        if (button?.CommandParameter is SecurityAlert selectedSecurityAlert) //! If the button clicked was a security alert
        {
            string securityAlertEdit = await DisplayPromptAsync("Edit Security Alert", "Edit the Security Alert:", initialValue: selectedSecurityAlert.AlertTitle); //! Prompt the user for input

            if (!string.IsNullOrWhiteSpace(securityAlertEdit))
            {
                selectedSecurityAlert.ChangeSecurityAlertName(securityAlertEdit);   //! Change the title of the alert
                securityAlertDB.EditSecurityAlert(selectedSecurityAlert);           //! Pass the editied alert to be u[pdated in the database table
                RefreshSecurityAlertsList();                                        //! Refresh the list of items in the user interface.
            }
        }
    }



    // Event handler for deleting a security alert
    private void DeleteSecurityAlert(object sender, EventArgs e) //! A method to delete the selected security alert.
    {
        Button button = sender as Button;

        if (button?.CommandParameter is SecurityAlert selectedSecurityAlert) //! If the button clicked is a security alert
        {
            securityAlertDB.DeleteSecurityAlert(selectedSecurityAlert.Id);  //! Delete the alert in the database that has this ID
            SecurityAlerts.Remove(selectedSecurityAlert);                   //! Remove the selected alert from the list
            RefreshSecurityAlertsList();                                    //! Refresh the list display.
        }


    }
}
```

## Testing
In the provided code, several methods have been tested in xunit to ensure their functionality.
Here's a breakdown of the methods that was tested.

Constructor (ViewSecurityAlertsPage()):
Tested that the SecurityAlerts collection is initialized.
Tested that the SecurityAlertDB instance is created.
Tested that the initial state of SecurityAlertsListview.ItemsSource is set correctly.

RefreshSecurityAlertsList() Method:
Tested that the method clears the SecurityAlerts collection.
Tested that it correctly adds new SecurityAlert objects to the collection.
Tested that it correctly reflects changes from the database.

CreateNewSecurityAlert(object sender, EventArgs e) Method:
Tested that a new SecurityAlert is created when the user provides valid input.
Tested that the method handles empty or null input appropriately.
Tested that the UI is correctly refreshed after creating a new alert.

SelectSecurityAlert(object sender, ItemTappedEventArgs e) Method:
Tested that the method correctly handles tapping on a SecurityAlert item.
Tested that the UI is updated after editing a selected alert.
Tested that the method handles null or invalid input.

EditSecurityAlert(object sender, EventArgs e) Method:
Tested that the method correctly handles editing a SecurityAlert item.
Tested that the UI is updated after editing an alert.
Tested that the method handles null or invalid input.

DeleteSecurityAlert(object sender, EventArgs e) Method:
Tested that the method correctly handles deleting a SecurityAlert item.
Tested that the UI is updated after deleting an alert.
Tested that the method handles null or invalid input.

## Code Review
I did 2 code reviews this week which is 1 more than usual. I know im not perfect at revieing other
peoples code yet but definatle improving. I did not see any code smells and only code good coding practices.

My code was revied, my feedback was that there is too many unnessassary comments to explain my code.
I dissagreed with the feedback, i felt that there just to much going on in the code and it needs short
explanations to help an other developer understand what is going on with ease. 

## Reflection
Over the past weeks, my journey in contributing to our team project on GitHub has been
marked by notable progress in both personal and team aspects, this has been a slow
learning curve to start with but feel it has been getting better. I also learned from speaking to my peers that by
inserting "csharp" at the start of my code snippet will add colour to my code in the repository.

Personal Growth:
In terms of code reviewing and GitHub navigation, I've experienced significant improvements.
The platform is becoming more enjoyable as I delve deeper into its functionalities.
One key realization has been the importance of adhering to coding principles. If i look back at
code i was producing before this modual it was very different, i have always felt i have had to
explain my code, but now it is alot clearer and the need for comments has reduced.

While I've become adept at crafting more efficient tests, the realm of mock testing has presented
a challenge. Acknowledging this, I am committed to dedicating more time to research and implementation,
aiming to have it seamlessly integrated into our project by the final report.

Team Workflow and Procedure Enhancements:
Collaboratively, our team has made commendable strides in the efficiency of issue resolution and code
review processes. Notably, there has been an uptick in active participation, with constructive feedback
becoming more commonplace. The team message comunication has ben more responsive in the spen of replys which
is great for team repport. This collective effort has contributed to a quicker turnaround in completing
tasks. I have found myself being able to complete more issues in and reviews in the same period of time.

Recognizing the need for improvement, I've identified disparities in my approach to error handling
and testing compared to my peers. This awareness serves as a catalyst for continuous improvement
in these areas.

In addressing common team challenges, we've initiated efforts to mitigate miscommunication.
Regular updates, where everyone shares their progress and challenges, have become a valuable practice.
Although participation in these conversations is not uniform, the mere initiation of such discussions
signifies an improvement in team communication.As I reflect on these aspects of my journey, the commitment
to continual learning and enhancement remains at the forefront. I look forward to further refining my
skills and contributing meaningfully to our collaborative efforts.
<br>