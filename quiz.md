<html>
<title>Pop Quiz on Sass</title>
<style>
    .FRQ{
        background-color: #3618c9;
    }
</style>
<form action="javascript:create_user()">
    <p><label class="FRQ">
        Input your username(does not have to be your real name):
        <input type="text" name="username" id="username" placeholder="Input username here" required>
    </label></p>
    <!-- Dummy questions. Change questions to Sass related later on. -->
    <p><label class="FRQ">
        Question 1: What is your favorite food?
        <input type="text" name="question1" id="question1" required>
    </label></p>
    <p><label class="FRQ">
        Question 2: What is your favorite game?
        <input type="text" name="question2" id="question2" required>
    </label></p>
    <p><label class="FRQ">
        Question 3: How many APs are you taking?
        <input type="text" name="question3" id="question3" required>
    </label></p>
    <p><label class="FRQ">
        Question 4: What is your hobby?
        <input type="text" name="question4" id="question4" required>
    </label></p>
    <p>
    <!-- Popup message on button click -->
        <button onclick="alert('Your answer have been posted!')" class="button">Submit</button>
    </p>
</form>

<script>
    const urlGame = "https://pythonalflask.tk/api/score";
    const createGame_fetch = urlGame + '/addScore';
    const urlRating = "https://pythonalflask.tk/api/rating";
    const createRating_fetch = urlRating + '/createRating'; 
    // Load users on page entry
    function create_user(){
        // Fix spam button issue
        // showScreen(SCREEN_DEFAULT);
        // Get the data
        const body = {
            username: document.getElementById("username").value,
            rating: document.getElementById("score").innerHTML
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
        fetch(createGame_fetch, requestOptions)
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