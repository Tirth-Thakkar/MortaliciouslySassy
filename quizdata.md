<h><strong>Snake High Scores</strong></h>
<table id="quizTable" style="width: 100%;">
    <tr>
        <th>Username</th>
        <th>Question 1 Response</th>
        <th>Question 2 Response</th>
        <th>Question 3 Response</th>
        <th>Question 4 Response</th>
        <th>Date of response</th>
    </tr>
  <tbody id="quizList">
  </tbody>
</table>

<script>
 // prepare HTML result container for new output
  const resultContainer = document.getElementById("quizList");
  // prepare URL's to allow easy switch from deployment and localhost
  const url = "http://192.168.37.91:8086/api/sass";
  const read_fetch = url + '/sassList';

  // Load users on page entry
  read_users();


  // Display User Table, data is fetched from Backend Database
  function read_users() {
    // prepare fetch options
    const read_options = {
      method: 'GET', // *GET, POST, PUT, DELETE, etc.
      mode: 'cors', // no-cors, *cors, same-origin
      cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
      credentials: 'omit', // include, *same-origin, omit
      headers: {
        'Content-Type': 'application/json'
      },
    };

    // fetch the data from API
    fetch(read_fetch, read_options)
      // response is a RESTful "promise" on any successful fetch
      .then(response => {
        // check for response errors
        if (response.status !== 200) {
            const errorMsg = 'Database read error: ' + response.status;
            console.log(errorMsg);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = errorMsg;
            tr.appendChild(td);
            resultContainer.appendChild(tr);
            return;
        }
        // valid response will have json data
      response.json().then(data => {
          console.log(data);
          data.sort(function(a, b) {
            return b.score - a.score;
          });
        for (let i = 0; i < 5; i++) {
          const row = data[i];
          console.log(row);
          add_row(row);
          }
        })
    })
    // catch fetch errors (ie ACCESS to server blocked)
    .catch(err => {
      console.error(err);
      const tr = document.createElement("tr");
      const td = document.createElement("td");
      td.innerHTML = err;
      tr.appendChild(td);
      resultContainer.appendChild(tr);
    });
  }

  function add_row(data) {
    const tr = document.createElement("tr");
    const username = document.createElement("td");
    const score = document.createElement("td");
    const dos = document.createElement("td");
  
    // obtain data that is specific to the API
    username.innerHTML = data.username; 
    question1.innerHTML = data.question1;
    question2.innerHTML = data.question2; 
    question3.innerHTML = data.question3; 
    question4.innerHTML = data.question4; 
    doquestion.innerHTML = data.doquestion;

    // add HTML to container
    tr.appendChild(username);
    tr.appendChild(question1);
    tr.appendChild(question2);
    tr.appendChild(question3);
    tr.appendChild(question4);
    tr.appendChild(doquestion);

    resultContainer.appendChild(tr);
  }
</script>