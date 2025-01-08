const parentContainer = document.getElementById('contentcenter');

// Find all relevant sibling elements under the parent container
const items = parentContainer.querySelectorAll('#contentcenter_specs_externalnav_wrapper');

// Array to store the extracted data
const extractedData = [];

// Loop through each item to extract desired content
items.forEach(wrapper => {
    // Get the text from `contentcenter_specs_externalnav_2`
    const externalNav2 = wrapper.querySelector('#contentcenter_specs_externalnav_2');
    const specsText = externalNav2 ? externalNav2.textContent.trim() : null;

    // Get the Model from the table in `contentcenter_specs_internalnav_2`
    const internalNav = wrapper.nextElementSibling;
    const release_date_row = internalNav.querySelector('tr:nth-child(1) > td:nth-child(2)'); // "Order" and Model column
    const release_date_text = release_date_row ? release_date_row.textContent.trim() : null;
     const discontinued_date_row = internalNav.querySelector('tr:nth-child(1) > td:nth-child(4)'); // "Order" and Model column
    const discontinued_date_text = discontinued_date_row ? discontinued_date_row.textContent.trim() : null;
    const orderRow = internalNav.querySelector('tr:nth-child(2) > td:nth-child(2)'); // "Order" and Model column
    const orderText = orderRow ? orderRow.textContent.trim() : null;
      const modelRow = internalNav.querySelector('tr:nth-child(2) > td:nth-child(4) > a'); // "Order" and Model column
    const modelText = modelRow ? modelRow.textContent.trim() : null;
    // Push the data into the array
    extractedData.push({
        specs: specsText,
        order: orderText,
        model: modelText,
        release_date: release_date_text,
        discontinued_date: discontinued_date_text
    });
});

// Output the extracted data
console.log(extractedData);