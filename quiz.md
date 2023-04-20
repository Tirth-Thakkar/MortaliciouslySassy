<html>
<h1>Pop Quiz on Sass</h1>
<h3>This is one of your assignments for the hacks</h3>
<style>
    .FRQ{
        /* background-color: #3618c9; */
        text-align: center;
    }
    .inputtext{
        text-align: center;
        border-width: 3px;
        border-style: solid;
        border-color: #000000;
        border-radius: 10px;
    }
</style>
<form action="javascript:create_user()">
    <p class="FRQ"><label>
        Input your username(does not have to be your real name):
        <br>
        <br>
        <input class="inputtext" type="text" name="username" id="username" placeholder="Input username here" required>
    </label></p>
    <!-- Dummy questions. Change questions to Sass related later on. -->
    <p class="FRQ"><label>
        Question 1: What is your favorite food?
        <br>
        <br>
        <input class="inputtext" type="text" name="question1" id="question1" placeholder="Input answer here" required>
    </label></p>
    <p class="FRQ"><label>
        Question 2: What is your favorite game?
        <br>
        <br>
        <input class="inputtext" type="text" name="question2" id="question2" placeholder="Input answer here" required>
    </label></p>
    <p class="FRQ"><label>
        Question 3: How many APs are you taking?
        <br>
        <br>
        <input class="inputtext" type="text" name="question3" id="question3" placeholder="Input answer here" required>
    </label></p>
    <p class="FRQ"><label>
        Question 4: What is your hobby?
        <br>
        <br>
        <input class="inputtext" type="text" name="question4" id="question4" placeholder="Input answer here" required>
    </label></p>
    <p>
    <!-- Popup message on button click -->
        <button onclick="alert('Your answer have been posted!')" class="form-button">Submit</button>
    </p>
</form>

<script>
    const urlSass = "http://206.188.196.247:8086/api/sass";
    const createSass_fetch = urlSass + '/addSass';
    // Load users on page entry
    function create_user(){
        const body = {
            username: document.getElementById("username").value,
            response1: document.getElementById("question1").value,
            response2: document.getElementById("question2").value,
            response3: document.getElementById("question3").value,
            response4: document.getElementById("question4").value
        };
        const requestOptions = {
            method: 'POST',
            body: JSON.stringify(body),
            mode: 'cors',
            cache: 'default',
            //credentials: 'include',
            headers: {
                "content-type": "application/json",
                'Authorization': 'Bearer my-token',
            },
        };
        // URL for Create API
        // Fetch API call to the database to create a new user
        fetch(createSass_fetch, requestOptions)
        .then(response => {
            // trap error response from Web API
            if (response.status !== 200) {
            const errorMsg = 'Database create error: ' + response.status;
            console.log(errorMsg);
            return;
            }
            // response contains valid result
            response.json().then(data => {
                console.log(data);
            })
        })
        }
</script>
</html>