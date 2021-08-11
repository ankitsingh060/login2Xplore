<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>LoginXplore learning</title>
    <style>
      *{
    padding: 0;
    margin: 0;
}

.container{

}
#empForm{
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    /* align-items: center; */
    background: beige;
    border-radius: 19px;
    width: 50%;
}
.container h2{
margin-left: 15%;
}
.form-group{
    font-size: 28px;
    display: flex;
    align-content: center;
    margin: 13px 10px;
    padding: 2px 4px;
    border-radius: 13px;
    background-color: black;
    background: none;
}
.form-group label{

}

.form-group input{
    font-size: 26px;
    border-radius: 14px;
    margin-left: 102px;
    opacity: 1.5;
}

.btn{
    width: 29%;
    font-size: 20px;
    border-radius: 13px;
    margin-left: 177px;
    margin-top: 32px;
}
    </style>
  </head>
  <body>
    <div class="container">
      <h2>Vertical (basic) form</h2>
      <form method="POST" id="empForm">
        <div class="form-group">
          <span
            ><label for="empId">Employee ID:</label><label id="empIdMsg"></label
          ></span>
          <input
            type="text"
            class="form-control"
            name="empId"
            id="empId"
            placeholder="Enter Employee Name"
          />
        </div>
        <div class="form-group">
          <span><label for="empName">Employee Name:</label> ></span>
          <input
            type="name"
            class="form-control"
            name="empName"
            id="empName"
            placeholder="Enter Employee Name"
          />
        </div>
        <div class="form-group">
          <label for="empEmail">Email:</label>
          <input
            type="email"
            class="form-control"
            id="empEmail"
            placeholder="Enter your Email"
          />
        </div>
        <input
          type="button"
          class="btn"
          id="empSave"
          value="save"
          onclick="saveEmployee()"
        />
      </form>
    </div>
    <script>
      function ValidateAndGetFormData() {
        var empIdVar = $("#empId").val();
        if (empIdVar === "") {
          alert("Employee ID Required Value");
          $("#empId").focus();
          return "";
        }

        var empNameVar = $("#empName").val();
        if (empNameVar === "") {
          alert("Employee Name is Requied Value");
          $("#empEmail").focus();
          return "";
        }
        var empEmailVar = $("#empEmail").val();
        if (empEmailVar === "") {
          alert("Employee Email is required Value");
          $("#empEmail").focus();
          return "";
        }
        var jsonStrObj = {
          empId: empIdVar,
          empName: empNameVar,
          empEmail: empEmailVar,
        };
        return JSON.stringify(jsonStrObj);
      }

      function createPUTRequest(connToken, jsonObj, dbName, relName) {
        var putReqStr = "{\n";
        +'\token":"' +
          connToken +
          '",' +
          '"dbName":"' +
          dbName +
          '",\n' +
          '"cmd" :"PUT",\n' +
          '"rel":"' +
          relName +
          '",' +
          '"jsonStr":\n' +
          jsonObj +
          "\n" +
          "}";
        return PUTRequest;
      }
      function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
        var url = dbBaseUrl + apiEndPointUrl;
        var jsonObj;
        $.post(url, reqString, function (result) {
          jsonObj = JSON.parse(result);
        }).fail(function (result) {
          var dataJsonObj = result.responseText;
          jsonObj = JSON.parse(dataJsonObj);
        });
        return jsonObj;
      }

      function saveEmployee() {
        var jsonStr = ValidateAndGetFormData();
        if (jsonStr === "") {
          return;
        }
        var putReqStr = createPUTRequest(
          "90936287|-31948850932777384|90945376",
          jsonStr,
          "SAMPLE",
          "EMP-REL"
        );

        alert(putReqStr);
        jQuery.ajaxSetup({ async: false });
        var resultObj = executeCommand(
          (putReqStr, "http://api.login2explore.com:5577", "/api/iml")
        );
        alert(JSON.stringify(resultObj));
        jQuery.ajaxSetup({ async: true });
        resetForm();
      }
    </script>
  </body>
</html>
