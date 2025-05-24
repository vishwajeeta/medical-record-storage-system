Yes! We can achieve this by creating a **"View Data"** button for each record. When the user clicks the button, a function will check if they have access using `checkAccess`. If access is granted, they will be redirected to the IPFS link; otherwise, an alert will be shown.  

---

## **🚀 Updated Code for Viewing IPFS Data**
```jsx
const checkAndViewData = async (recordId, ipfsLink) => {
  if (!contract || !account) return alert("Please connect wallet first");

  try {
    const hasAccess = await contract.checkAccess(recordId, userDID); // Replace userDID with the actual DID
    console.log("Access Check:", hasAccess);

    if (hasAccess) {
      window.open(ipfsLink, "_blank"); // Open IPFS link in a new tab
    } else {
      alert("Access Denied! You do not have permission to view this data.");
    }
  } catch (error) {
    console.error("Error checking access", error);
    alert("Failed to check access");
  }
};
```

---

## **🔹 Integrate in JSX**
Modify the **record listing** to include this button:
```jsx
{records.map((record) => (
  <div key={record.id} style={{ marginBottom: "10px", border: "1px solid #ccc", padding: "10px" }}>
    <p><strong>Owner DID:</strong> {record.ownerDID}</p>
    <p><strong>Data Hash:</strong> {record.dataHash}</p>
    <button onClick={() => checkAndViewData(record.id, record.ipfsLink)}>
      View Data
    </button>
  </div>
))}
```

---

## **✅ How It Works**
1. **User clicks "View Data" button** for a record.  
2. **`checkAndViewData(recordId, ipfsLink)` is called**, checking access using `checkAccess(recordId, userDID)`.  
3. If **access is granted**, the IPFS link opens in a **new tab**.  
4. If **access is denied**, an alert informs the user.  

---

This ensures **secure access control** while keeping the UI intuitive! 🎯 🚀 Let me know if you need any modifications! 😊