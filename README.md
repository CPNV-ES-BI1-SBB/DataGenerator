# DataGenerator
Part of BI project - 2024 - SBB.
## Description
A Data Fetcher / Data Generator for a Bussiness Inteligence project.
## Dependencies / run
- Language: Ruby
- API: Sinatra
- HTTP Client: HTTParty
## API
### Routes
// TODO define what and how the "clients" will want the data. (Clients are the Extract team)
#### JSON
```JSON
{
  "stop": {
    "id": "8503283",
    "name": "Einsiedeln",
    "type": "train,strain",
    "x": "699076",
    "y": "220557",
    "lon": 8.744481,
    "lat": 47.128578
  },
  "connections": [
    {
      "time": "2024-12-06 14:45:00",
      "*G": "S",
      "*L": "40",
      "*Z": "016955",
      "type": "strain",
      "line": "S40",
      "operator": "SOB-sob",
      "color": "039~fff~",
      "type_name": "S-Train",
      "terminal": {
        "id": "8503110",
        "name": "Rapperswil SG",
        "x": 704370,
        "y": 231356,
        "lon": 8.816743,
        "lat": 47.224885
      }
    }
  ]
}
```
#### PDF

The PDF will be generated with the data from the Search.ch API.

Using the Prawn Library, the PDF will be generated with the following structure:

- Header
  - Station name (Gare de `{{station}}`)
  - Date (État au `{{date}}`)
  - Logo (SBB)
- Body
  - Table
    - Columns
      - Time
      - Line
      - Destination
      - Vias
      - Platform

Example: [Timetable for Yverdon-les-Bains](docs/examples/yverdon-les-bains_24-12-12.pdf)

Usage Example:
```Ruby
api = SearchAPI.new
response = api.get_stationboard({:stop => "Yverdon-les-Bains", :date => "12/12/2024"})

pdf = PDFFormater.new
pdf.format(response[:formatted_response])
```

Return:
```
%PDF-1.4
%\xFF\xFF\xFF\xFF
1 0 obj
<< /Creator <feff0050007200610077006e>
/Producer <feff0050007200610077006e>
...
```


## Source API
Search.ch : https://search.ch/timetable/api/help
## Testing
RSpec

```Ruby
RSpec.describe "An example" do
  it "adds two numbers" do
    expect(1 + 1).to eq(2)
  end

  it "raises an error when dividing by zero" do
    expect { 1 / 0 }.to raise_error(ZeroDivisionError)
  end
end
```
