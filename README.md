# apiTest
import React, { useState, useEffect } from "react";
import axios from "axios";

const ApiTest = () => {
  const styles = {
    display: "inline",
    width: "30%",
    height: 50,
    float: "left",
    padding: 5,
    border: "0.5px solid black",
    marginBottom: 10,
    marginRight: 10,
  };

  const [allData, setAllData] = useState([]);
  const [filteredData, setFilteredData] = useState(allData);

  const handleSearch = (event) => {
    let value = event.target.value.toLowerCase();
    let result = [];
    console.log(value);
    result = allData.filter((data) => {
      return data.addr1.search(value) !== -1;
    });
    setFilteredData(result);
  };

  useEffect(() => {
    axios(
      "http://api.visitkorea.or.kr/openapi/service/rest/GoCamping/basedList?ServiceKey=DBx1v7ble2j4MNFWznYeeM5wQYthH5QTVeMOTXn5H%2FxvLP7Bbaa8IZvKxHq8r0425fyEMXvrs32EFDRIALvz5A%3D%3D&numOfRows=10&pageNo=1&MobileOS=ETC&MobileApp=TestApp&_type=json"
    )
      .then((response) => {
        console.log(response.data.response.body.items.item);
        setAllData(response.data.response.body.items.item);
        setFilteredData(response.data.response.body.items.item);
      })
      .catch((error) => {
        console.log("Error getting fake data: " + error);
      });
  }, []);

  return (
    <div className="App">
      <div style={{ margin: "0 auto", marginTop: "10%" }}>
        <label>Search:</label>
        <input type="text" onChange={(event) => handleSearch(event)} />
      </div>
      <div style={{ padding: 10 }}>
        {filteredData.map((value, index) => {
          return (
            <div style={styles} key={value.contentId}>
              {value.addr1}
            </div>
          );
        })}
      </div>
    </div>
  );
};

export default ApiTest;
