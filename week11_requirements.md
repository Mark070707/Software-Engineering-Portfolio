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
Initial State of SecurityAlertsListview.ItemsSource:
Tested that the initial state of SecurityAlertsListview.ItemsSource is set correctly.

RefreshSecurityAlertsList() Method:
Tested that the method clears the SecurityAlerts collection.
Tested that it correctly adds new SecurityAlert objects to the collection.
Reflecting Changes from the Database:
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
I did 1 code review this week which is 1 less than usuallast time as my p[eers were slow at submitting there work.
I I did not see any code smells and only code good coding practices. I think everyone has taken on feedback from
prevoius code reviews and put them into action and not repeating early mistakes.

My code was revied and they just said no problems found.

## Reflection
In recent weeks, my engagement with our team project on GitHub has seen substantial growth both on a personal
level and within the team dynamics. While the initial learning curve was gradual, I've noticed significant progress.
An interesting tip I gathered from my peers is that adding "csharp" at the beginning of code snippets enhances the
code's appearance in the repository.

Personal Growth:
In terms of code reviewing and navigating GitHub, I've made noteworthy strides. The GitHub platform has become more
enjoyable as I explore its functionalities. One pivotal realization is the significance of adhering to coding principles.
Looking back at my code before this module, I see a notable difference. I've always emphasized explaining my code,
and now it's clearer, reducing the need for excessive comments. Testing has slightly improved at crafting efficient tests.

Team Workflow and Procedure Enhancements:
Collaboratively, our team has achieved commendable efficiency in issue resolution and code review processes.
There's an increase in active participation, with constructive feedback becoming more commonp. The team's
message communication has become more responsive, usually comunication has ben left till the last hours before
submission nevertheless it has improved. This collective effort has led to a quicker
turnaround in completing tasks, allowing me to handle more issues and reviews within the same timeframe.

Recognizing the need for improvement, the agile devepopement sprints has suited this project well, however i understand
the need for teams roles such as project manager, superviser, tester and so on. This would help when decisions ned to
be made from the collection of ideas that team members bring to the table. Perhaps the use of more planning software
like Gant would helpl manage the time scales and milestone of this project and help us visulise our path. I think
daily stand up meeting would enhance every area of the teams progress on the project with moral, errors and helping
one another.

As I reflect on these aspects of my journey, the commitment to continual learning and enhancement remains at the forefront.
I look forward to further refining my skills and contributing meaningfully to our collaborative efforts. My biggest takeaway
from this module is the module is the practice of good coding principles. I feel that it sould not matter who has
written the code, if they follow the good coding principles it should be perfectly readable and maintainable.