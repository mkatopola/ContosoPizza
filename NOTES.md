===============================================================

GitHub Link: https://github.com/mkatopola/ContosoPizza

EXISTING CONTENT

[
  {
    "id": 1,
    "name": "Classic Italian",
    "isGlutenFree": false
  },
  {
    "id": 2,
    "name": "Veggie",
    "isGlutenFree": true
  }
]

ADDED CONTENT

[
  {
    "id": 3,
    "name": "Pepperoni",
    "isGlutenFree": false
  },
  {
    "id": 4,
    "name": "Boston Pizza",
    "isGlutenFree": true
  },
  {
    "id": 5,
    "name": "Cheese",
    "isGlutenFree": true
  },
  {
    "id": 6,
    "name": "BBQ Chicken",
    "isGlutenFree": true
  }
]

===============================================================

GitHub Link: https://github.com/mkatopola/mslearn-dotnet-files

Part 2: Sales Summary Function

void GenerateSalesSummaryReport(IEnumerable<string> salesFiles, double salesTotal, string outputDirectory)
{
    List<string> salesSummary = new()
    {
        "Sales Summary",
        "----------------------------",
        $"Total Sales: {FormatCurrency(salesTotal)}",
        "",
        "Details:"
    };

    foreach (var file in salesFiles)
    {
        if (Path.GetFileName(file) != "sales.json")
        {
            continue;
        }
        
        var data = JsonConvert.DeserializeObject<SalesData>(File.ReadAllText(file));

        salesSummary.Add(
            $"  {Path.GetFileName(file)}: {FormatCurrency(data?.Total ?? 0)}");
    }

    File.WriteAllText(
        Path.Combine(outputDirectory, "salesSummary.txt"),
        string.Join(Environment.NewLine, salesSummary));
}

string FormatCurrency(double amount) =>
    $"${amount:N2}";
