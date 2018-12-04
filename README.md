# miniature-telegram
GAS - Compare folder list to needed list and create missing folders

You will need a sheet to place information from the two lists. It will include a few formulas, described here.

This script is set up to specfically use the ePM All Projects Info Report, and to create folders in our Regional Repository for each
new project. You will need to modify it, at least slightly, for use in YOUR region.

Set up a google spreadsheet, and make three sheets named "Folders", "Projects", and "Lookups".

"Folders", D1 - "Duplicate Folders"
"Folders", D2 - =arrayformula(unique(iferror(filter(B2:B,B2:B<>"",countif(B2:B,$B$2:$B)>1),"")))

"Projects", A1 - "Folder"
"Projects", A2 - =arrayformula(if(B2:B<>"",iferror(vlookup(B2:B,{Folders!B:B,Folders!A:A},2,false),"NO FOLDER"),""))
"Projects", F1 - "SPM Email"
"Projects", F2 - =arrayformula(if(E2:E<>"",vlookup(E2:E,Lookups!A:C,2,false),""))
"Projects", G1 - "Branch Manager Email"
"Projects", G2 - =arrayformula(if(E2:E<>"",vlookup(E2:E,Lookups!A:C,3,false),""))
"Projects", H1 - "Notification List"
"Projects", H2 - =arrayformula(if(D2:D<>"",D2:D&" "&F2:F&" "&G2:G,""))

"Lookups", A:A - List of Managing Orgs in your Region
"Lookups", B:B - The Supervisor (or other person to be notified) for the Managing Org
"Lookups", C:C - The Branch Manager (or second person to be notified) for the Managing Org
