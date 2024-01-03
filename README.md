# AICP TASK 7
#include <iostream>
#include <iomanip>
#include <vector>
#include <algorithm>

using namespace std;

const int NUM_CHARITIES = 3;

void setupDonationSystem(vector<string>& charityNames, vector<double>& charityTotals);
void recordAndTotalDonation(const vector<string>& charityNames, vector<double>& charityTotals);
void showTotals(const vector<string>& charityNames, const vector<double>& charityTotals);

int main() 
{
    vector<string> charityNames(NUM_CHARITIES);
    vector<double> charityTotals(NUM_CHARITIES, 0.0);

    setupDonationSystem(charityNames, charityTotals);

    cout << "\nTask 2 - Record and total each donation\n";
    recordAndTotalDonation(charityNames, charityTotals);

    cout << "\nTask 3 - Show the totals so far\n";
    showTotals(charityNames, charityTotals);

    return 0;
}

void setupDonationSystem(vector<string>& charityNames, vector<double>& charityTotals) 
{
    cout << "Task 1 - Set up the donation system\n";

    for (int i = 0; i < NUM_CHARITIES; ++i) 
	{
        cout << "Enter the name of charity " << i + 1 << ": ";
        cin >> charityNames[i];
        charityTotals[i] = 0.0;
    }

    cout << "\nCharities available for donation:\n";
    for (int i = 0; i < NUM_CHARITIES; ++i) 
	{
        cout << i + 1 << ". " << charityNames[i] << endl;
    }
}

void recordAndTotalDonation(const vector<string>& charityNames, vector<double>& charityTotals) 
{
    int choice;
    double shoppingBill;
    double donation;

    while (true) 
	{
        cout << "Enter the charity choice (1, 2, 3) or -1 to finish: ";
        cin >> choice;

        if (choice == -1) 
		{
            break;
        } else if (choice >= 1 && choice <= NUM_CHARITIES) 
		{
            cout << "Enter the value of the customer's shopping bill: $";
            cin >> shoppingBill;

            donation = shoppingBill * 0.01;
            charityTotals[choice - 1] += donation;

            cout << fixed << setprecision(2);
            cout << "Donated $" << donation << " to " << charityNames[choice - 1] << endl;
        } else 
		{
            cout << "Invalid charity choice. Please enter 1, 2, 3, or -1.\n";
        }
    }
}

void showTotals(const vector<string>& charityNames, const vector<double>& charityTotals) 
{
    vector<pair<double, string>> sortedCharities;

    for (int i = 0; i < NUM_CHARITIES; ++i) 
	{
        sortedCharities.push_back({charityTotals[i], charityNames[i]});
    }

    sort(sortedCharities.rbegin(), sortedCharities.rend());

    double grandTotal = 0.0;

    for (const auto& entry : sortedCharities) 
	{
        cout << entry.second << ": $" << entry.first << endl;
        grandTotal += entry.first;
    }

    cout << "\nGRAND TOTAL DONATED TO CHARITY: $" << grandTotal << endl;
}
 
