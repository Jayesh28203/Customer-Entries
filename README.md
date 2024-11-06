<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Customer Form</title>
    <script src="https://cdn.sheetjs.com/xlsx-latest/package/dist/xlsx.full.min.js"></script>
    <style>
        /* Simple styling */
        form {
            max-width: 300px;
            margin: auto;
        }
        input, button {
            display: block;
            width: 100%;
            margin: 10px 0;
            padding: 8px;
        }
    </style>
</head>
<body>
    <h2>Customer Form</h2>
    <form id="customerForm">
        <label for="name">Customer Name:</label>
        <input type="text" id="name" name="name" required>

        <label for="caf_id">CAF ID:</label>
        <input type="text" id="caf_id" name="caf_id" required>

        <label for="mobile">Mobile Number:</label>
        <input type="tel" id="mobile" name="mobile" required>

        <button type="button" onclick="addData()">Add</button>
        <button type="button" onclick="submitData()">Submit</button>
    </form>

    <script>
        // Initialize an array for storing form data
        let data = [["Customer Name", "CAF ID", "Mobile Number"]];

        function addData() {
            // Get form values
            const name = document.getElementById("name").value;
            const cafId = document.getElementById("caf_id").value;
            const mobile = document.getElementById("mobile").value;

            // Validate inputs
            if (name && cafId && mobile) {
                // Add data to array
                data.push([name, cafId, mobile]);

                // Clear form fields
                document.getElementById("customerForm").reset();
                alert("Data added successfully!");
            } else {
                alert("Please fill in all fields.");
            }
        }

        function submitData() {
            if (data.length > 1) { // Ensure there is data beyond the headers
                // Create a new workbook and add data
                const wb = XLSX.utils.book_new();
                const ws = XLSX.utils.aoa_to_sheet(data);
                XLSX.utils.book_append_sheet(wb, ws, "Customers");

                // Export to Excel
                XLSX.writeFile(wb, "CustomerData.xlsx");
                alert("Data exported to Excel!");

                // Clear the data array (except headers)
                data = [["Customer Name", "CAF ID", "Mobile Number"]];
            } else {
                alert("No data to submit.");
            }
        }
    </script>
</body>
</html>
