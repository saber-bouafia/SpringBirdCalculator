    //rate change
      let EuroToGBP = 0.8823; // 0.86 * 1.0295; //0.8823
      let CHFToGBP = 0.932; //0.9 * 1.0295;

      // Fees (in Euro)
      const feesEuro = {
        euipoEuro: { baseEuro: 850, secondEuro: 50, additionalEuro: 150 },
        wipoEuro: {
          AppEUEuro: {
            baseEuro: 850,
            colourEuro: 950, //
            secondEuro: 50,
            additionalEuro: 150,
          },
          ourEuro: { base: 475, additional: 50 },
          subsequentDesignationEuro: 0.0,
        },
      };

      // Fees (in CHF)
      const feesCHF = {
        wipoCHF: {
          newAppEUCHF: { base: 789, second: 48, additional: 144 },
          newAppCHF: { base: 635, colour: 903 },
        },
        subsequentDesignationCHF: 300,
      };

      // Fees (in GBP)
      //Q4.
      const fees = {
        ukipo: { base: 170, additional: 50 },
        ukOur: { base: 520, additional: 100 },
        euipo: {
          base: feesEuro.euipoEuro.baseEuro * EuroToGBP,
          second: feesEuro.euipoEuro.secondEuro,
          additional: feesEuro.euipoEuro.additionalEuro,
        },
        euOur: { base: 695, second: 50, additional: 95 },
        wipo: {
          AppEU: {
            base: EuroToGBP * feesEuro.wipoEuro.AppEUEuro.baseEuro, // £714
            colour: EuroToGBP * feesEuro.wipoEuro.AppEUEuro.colourEuro, // £798
            second: EuroToGBP * feesEuro.wipoEuro.AppEUEuro.secondEuro, // €50
            additional: EuroToGBP * feesEuro.wipoEuro.AppEUEuro.additionalEuro, // €150
          },
          our: { base: 475, second: 50, additional: 150 },
          newApp: {
            base: CHFToGBP * feesCHF.wipoCHF.newAppCHF.base,
            colour: CHFToGBP * feesCHF.wipoCHF.newAppCHF.colour,
          },
          newAppEU: {
            base: CHFToGBP * feesCHF.wipoCHF.newAppEUCHF.base,
            second: CHFToGBP * feesCHF.wipoCHF.newAppEUCHF.second,
            additional: CHFToGBP * feesCHF.wipoCHF.newAppEUCHF.additional,
          }, //789CHF
          subsequentDesignation: feesCHF.subsequentDesignationCHF * CHFToGBP, // £264 (300CHF)
          ourSequentDesignation: { base: 350, additional: 150 },
        },
        overseas: { base: 450, additional: 50 },
        throughtheUKoffice: { base: 40 },
        OurfeesEUdesignation: { base: 150 },
      };

      // Main calculation function
      function calculateCost() {
        const region = document.querySelector(
          'input[name="region"]:checked'
        )?.value;
        let classes = parseInt(document.getElementById("classesSelect").value);
        const q1 = document.querySelector('input[name="q1"]:checked')?.value;
        const q2 = document.querySelector('input[name="q2"]:checked')?.value;
        const q3 = document.querySelector('input[name="q3"]:checked')?.value;
        const q4 = document.querySelector('input[name="q4"]:checked')?.value;
        const q5 = document.querySelector('input[name="q5"]:checked')?.value;
        const q6 = document.querySelector('input[name="q6"]:checked')?.value;

        let totalCost = 0;

        if (region === "UK") {
          //if UK selected
          // UKIPO fees: £170 for 1 class; additional £50 per extra class.
          // Our fees: £520 for 1 class; additional £100 per extra class.
          totalCost = 170 + 520; // £170 + £520
          if (classes > 1) {
            totalCost += (classes - 1) * (50 + 100);
          }
        } else if (region === "EU") {
          //if EU selected
          if (q1 === "no" && q2 === "no") {
            //Q1. Do you already have an international application? NO
            //Q2. Will you also want to protect the mark in other countries soon? NO
            totalCost = 695 + 850 * EuroToGBP; // €850 + £695 = £1345
            q4 === "yes"; //Q4. Is the mark you want to protect in colour?
            if (classes > 1) {
              //€50 for the second + £50
              totalCost += 50 * EuroToGBP + 50;
              if (classes > 2) {
                totalCost += 150 * EuroToGBP + 95;
                if (classes > 3) {
                  totalCost += (classes - 3) * (95 + 150 * EuroToGBP);
                }
              }
            }
          } else if (q1 === "no" && q2 === "yes" && q3 === "yes") {
            //Q1. Do you already have an international application? NO
            //Q2. Will you also want to protect the mark in other countries soon? YES
            //Q3. Do you have a UK Registration already? YES
            //Q4. Is the mark you want to protect in colour?
            totalCost =
              q4 === "yes"
                ? 375 + 903 * CHFToGBP + 40 + 150 + 789 * CHFToGBP //Q4. YES
                : 375 + 653 * CHFToGBP + 40 + 150 + 789 * CHFToGBP; //Q4. NO

            if (classes > 1) {
              totalCost += 50 + 48 * CHFToGBP;
              if (classes > 2) {
                console.log(totalCost);
                totalCost += 50 + 144 * EuroToGBP;
                if (classes > 3) {
                  totalCost += (classes - 3) * (50 + 144 * EuroToGBP);
                }
              }
            }
          } else if (q1 === "no" && q2 === "yes" && q3 === "no") {
            //Q1. Do you already have an international application? NO
            //Q2. Will you also want to protect the mark in other countries soon? YES
            //Q3. Do you have a UK Registration already? NO
            totalCost =
              q4 === "yes"
                ? 375 + 903 * CHFToGBP + 40 + 150 + 789 * CHFToGBP + 170 + 520 //Q4. YES
                : 375 + 653 * CHFToGBP + 40 + 150 + 789 * CHFToGBP + 170 + 520; //Q4. NO

            if (classes > 1) {
              totalCost += 50 + 48 * CHFToGBP + 50 + 100;
              if (classes > 2) {
                console.log(totalCost);
                totalCost += 50 + 144 * EuroToGBP + 50 + 100;
                if (classes > 3) {
                  totalCost +=
                    (classes - 3) * (50 + 144 * EuroToGBP + 50 + 100);
                }
              }
            }
          } else if (q1 === "yes") {
            //Q1. Do you already have an international application? Yes
            totalCost = 300 * CHFToGBP + 275;
            if (classes > 1) {
              totalCost += (classes - 1) * 50;
            }
          }
        }

        document.getElementById(
          "totalCost"
        ).textContent = `Total Cost: £${Math.round(totalCost.toFixed(2))}`;

        // World countries calculation
        if (region === "other") {
          document.getElementById("worldTotalCost").classList.remove("hidden");
          document.getElementById("totalCost").classList.add("hidden");
        } else {
          document.getElementById("worldTotalCost").classList.add("hidden");
          document.getElementById("totalCost").classList.remove("hidden");
        }
      }

      // Event listeners
      document.querySelectorAll('input[type="radio"], select').forEach((el) => {
        el.addEventListener("change", calculateCost);
      });

      // Load the calculator on page load
      calculateCost();

      const wipoDropdownToggle = document.getElementById("wipoDropdownToggle");
      const wipoDropdownOptions = document.getElementById(
        "wipoDropdownOptions"
      );
      const nationalDropdownToggle = document.getElementById(
        "nationalDropdownToggle"
      );
      const nationalDropdownOptions = document.getElementById(
        "nationalDropdownOptions"
      );
      const WIPOselectedCountriesElement = document.getElementById(
        "WIPOselectedCountries"
      );
      const NationalselectedCountriesElement = document.getElementById(
        "NationalselectedCountries"
      );

      let wipoCountriesData = [];
      let nationalCountriesData = [];

      // Fetch WIPO countries data
      fetch(
        "https://cdn.jsdelivr.net/gh/saber-bouafia/SpringBirdCalculator/wipo_countries.json"
      )
        .then((response) => response.json())
        .then((data) => {
          wipoCountriesData = data;
          data.sort((a, b) => a.Country.localeCompare(b.Country));
          data.forEach((item) => {
            const listItem = document.createElement("li");
            listItem.innerHTML = `
                    <input type="checkbox" value="${item.Country}" data-country="${item.Country}" />
                    ${item.Country}
                  `;
            wipoDropdownOptions.appendChild(listItem);
          });
        })
        .catch((error) =>
          console.error("Error fetching WIPO country data:", error)
        );

      // Fetch National countries data
      fetch(
        "https://cdn.jsdelivr.net/gh/saber-bouafia/SpringBirdCalculator/national_countries.json"
      )
        .then((response) => response.json())
        .then((data) => {
          nationalCountriesData = data;
          data.sort((a, b) => a.Country.localeCompare(b.Country));
          data.forEach((item) => {
            const listItem = document.createElement("li");
            listItem.innerHTML = `
                    <input type="checkbox" value="${item.Country}" data-country="${item.Country}" />
                    ${item.Country}
                  `;
            nationalDropdownOptions.appendChild(listItem);
          });
        })
        .catch((error) =>
          console.error("Error fetching National country data:", error)
        );

      // Toggle dropdown visibility
      wipoDropdownToggle.addEventListener("click", () => {
        wipoDropdownOptions.classList.toggle("hidden");
      });

      nationalDropdownToggle.addEventListener("click", () => {
        nationalDropdownOptions.classList.toggle("hidden");
      });

      let totalWIPOComplementaryFee = 0;
      let totalWIPOOneClassFee = 0;
      let totalWIPOSecondClassFee = 0;
      let totalWIPOThirdClassFee = 0;
      let totalWIPOEachAdditionalUpTo5 = 0;
      let totalWIPOThreeClassesFee = 0;
      let totalWIPOAdditionalClassFee = 0;
      let totalWIPOAdditionalClassOver10Fee = 0;
      let totalWIPOSecondPartforeachClassFee = 0;

      let selectedWIPOCountriesCount = 0;
      let selectedNationalCountriesCount = 0;
      // Update WIPO selection when checkboxes are clicked
      function updateWIPOselectedCountries() {
        const wipoCheckboxes = wipoDropdownOptions.querySelectorAll(
          'input[type="checkbox"]'
        );
        const selected = Array.from(wipoCheckboxes)
          .filter((checkbox) => checkbox.checked)
          .map((checkbox) => checkbox.dataset.country);

        WIPOselectedCountriesElement.textContent = selected.length
          ? selected.join(", ")
          : "None";

        WIPOselectedCountriesElement.textContent = selected.length
          ? selected.join(", ")
          : "None";
        selectedWIPOCountriesCount = selected.length; // Store count globally

        totalWIPOComplementaryFee = 0;
        totalWIPOOneClassFee = 0;
        totalWIPOSecondClassFee = 0;
        totalWIPOThirdClassFee = 0;
        totalWIPOEachAdditionalUpTo5 = 0;
        totalWIPOThreeClassesFee = 0;
        totalWIPOAdditionalClassFee = 0;
        totalWIPOAdditionalClassOver10Fee = 0;
        totalWIPOSecondPartforeachClassFee = 0;

        selected.forEach((country) => {
          const countryData = wipoCountriesData.find(
            (item) => item.Country === country
          );
          if (countryData) {
            totalWIPOComplementaryFee +=
              parseFloat(countryData["Complementary Fee"]) || 0;
            totalWIPOOneClassFee +=
              parseFloat(countryData["for one class"]) || 0;
            totalWIPOAdditionalClassFee +=
              parseFloat(countryData["for each additional class"]) || 0;
            totalWIPOSecondClassFee +=
              parseFloat(countryData["for second class"]) || 0;
            totalWIPOThirdClassFee +=
              parseFloat(countryData["for third class"]) || 0;
            totalWIPOEachAdditionalUpTo5 +=
              parseFloat(countryData["for each additional up to 5"]) || 0;
            totalWIPOThreeClassesFee +=
              parseFloat(countryData["for three classes"]) || 0;
            totalWIPOAdditionalClassOver10Fee +=
              parseFloat(countryData["for each additional over 10"]) || 0;
            totalWIPOSecondPartforeachClassFee +=
              parseFloat(countryData["Second part for each class"]) || 0;
          }
        });

        console.log("WIPO Countries Totals:");
        console.log(
          `Total WIPO Complementary Fee: ${totalWIPOComplementaryFee}`
        );
        console.log(`Total WIPO One Class Fee: ${totalWIPOOneClassFee}`);
        console.log(
          `Total WIPO Additional Class Fee: ${totalWIPOAdditionalClassFee}`
        );
        console.log(`Total WIPO Second Class Fee: ${totalWIPOSecondClassFee}`);
        console.log(`Total WIPO Third Class Fee: ${totalWIPOThirdClassFee}`);
        console.log(
          `Total WIPO Each Additional Up To 5: ${totalWIPOEachAdditionalUpTo5}`
        );
        console.log(
          `Total WIPO Three Classes Fee: ${totalWIPOThreeClassesFee}`
        );
        console.log(
          `Total WIPO Additional Class Over 10 Fee: ${totalWIPOAdditionalClassOver10Fee}`
        );
        console.log(
          `Total WIPO Second Part for each Class Fee: ${totalWIPOSecondPartforeachClassFee}`
        );
      }

      let totalNationalComplementaryFee = 0;
      let totalNationalOneClassFee = 0;
      let totalNationalSecondClassFee = 0;
      let totalNationalThirdClassFee = 0;
      let totalNationalEachAdditionalUpTo5 = 0;
      let totalNationalThreeClassesFee = 0;
      let totalNationalAdditionalClassFee = 0;
      let totalNationalAdditionalClassOver10Fee = 0;
      let totalNationalSecondPartforeachClassFee = 0;

      // Update National selection when checkboxes are clicked
      function updateNationalselectedCountries() {
        const nationalCheckboxes = nationalDropdownOptions.querySelectorAll(
          'input[type="checkbox"]'
        );
        const selected = Array.from(nationalCheckboxes)
          .filter((checkbox) => checkbox.checked)
          .map((checkbox) => checkbox.dataset.country);

        NationalselectedCountriesElement.textContent = selected.length
          ? selected.join(", ")
          : "None";

        NationalselectedCountriesElement.textContent = selected.length
          ? selected.join(", ")
          : "None";
        selectedNationalCountriesCount = selected.length; // Store count globally

        // Reset the totals before recalculating

        totalNationalComplementaryFee = 0;
        totalNationalOneClassFee = 0;
        totalNationalSecondClassFee = 0;
        totalNationalThirdClassFee = 0;
        totalNationalEachAdditionalUpTo5 = 0;
        totalNationalThreeClassesFee = 0;
        totalNationalAdditionalClassFee = 0;
        totalNationalAdditionalClassOver10Fee = 0;
        totalNationalSecondPartforeachClassFee = 0;

        selected.forEach((country) => {
          const countryData = nationalCountriesData.find(
            (item) => item.Country === country
          );
          if (countryData) {
            totalNationalComplementaryFee +=
              parseFloat(countryData["Complementary Fee"]) || 0;
            totalNationalOneClassFee +=
              parseFloat(countryData["for one class"]) || 0;
            totalNationalAdditionalClassFee +=
              parseFloat(countryData["for each additional class"]) || 0;
            totalNationalSecondClassFee +=
              parseFloat(countryData["for second class"]) || 0;
            totalNationalThirdClassFee +=
              parseFloat(countryData["for third class"]) || 0;
            totalNationalEachAdditionalUpTo5 +=
              parseFloat(countryData["for each additional up to 5"]) || 0;
            totalNationalThreeClassesFee +=
              parseFloat(countryData["for three classes"]) || 0;
            totalNationalAdditionalClassOver10Fee +=
              parseFloat(countryData["for each additional over 10"]) || 0;
            totalNationalSecondPartforeachClassFee +=
              parseFloat(countryData["Second part for each class"]) || 0;
          }
        });

        console.log("National Countries Totals:");
        console.log(
          `Total National  Complementary Fee: ${totalNationalComplementaryFee}`
        );
        console.log(
          `Total National One Class Fee: ${totalNationalOneClassFee}`
        );
        console.log(
          `Total National Additional Class Fee: ${totalNationalAdditionalClassFee}`
        );
        console.log(
          `Total National Second Class Fee: ${totalNationalSecondClassFee}`
        );
        console.log(
          `Total National Third Class Fee: ${totalNationalThirdClassFee}`
        );
        console.log(
          `Total National Each Additional Up To 5: ${totalNationalEachAdditionalUpTo5}`
        );
        console.log(
          `Total National Three Classes Fee: ${totalNationalThreeClassesFee}`
        );
        console.log(
          `Total National Additional Class Over 10 Fee: ${totalNationalAdditionalClassOver10Fee}`
        );
        console.log(
          `Total National Second Part for each Class Fee: ${totalNationalSecondPartforeachClassFee}`
        );
      }

      wipoDropdownOptions.addEventListener(
        "change",
        updateWIPOselectedCountries
      );
      nationalDropdownOptions.addEventListener(
        "change",
        updateNationalselectedCountries
      );
      // Rest of the existing JavaScript code for calculations and event listeners...

      //Logic for "Others"
      function calculateOtherCost() {
        const region = document.querySelector(
          'input[name="region"]:checked'
        )?.value;
        if (region !== "other") return;

        const classes = parseInt(
          document.getElementById("classesSelect").value
        );
        const q1 = document.querySelector('input[name="q1"]:checked')?.value;
        const q3 = document.querySelector('input[name="q3"]:checked')?.value;
        const q4 = document.querySelector('input[name="q4"]:checked')?.value;
        const q6 = document.querySelector('input[name="q6"]:checked')?.value;

        let totalCost = 0;
        console.log("Others");

        if (
          typeof totalNationalOneClassFee !== "number" ||
          isNaN(totalNationalOneClassFee)
        ) {
          console.error("totalNationalOneClassFee is not a valid number");
          return;
        }

        // Ensure totaWIPOOneClassFee is defined and a number
        if (
          typeof totalWIPOOneClassFee !== "number" ||
          isNaN(totalWIPOOneClassFee)
        ) {
          console.error("totalWIPOOneClassFee is not a valid number");
          return;
        }
        if (q6 === "no") {
          console.log("totalNationalOneClassFee:", totalNationalOneClassFee);

          // Ensure totalNationalOneClassFee is defined and a number

          // National Type
          totalCost += 450 + totalNationalOneClassFee; // Our base fee for first class

          if (classes > 1) {
            totalCost +=
              totalNationalOneClassFee +
              totalNationalSecondClassFee +
              selectedNationalCountriesCount * 150;

            if (classes > 2) {
              totalCost +=
                totalNationalOneClassFee +
                totalNationalSecondClassFee +
                totalNationalThirdClassFee +
                totalNationalThreeClassesFee +
                selectedNationalCountriesCount * 150;
            }
            if (classes > 4) {
              totalCost +=
                (classes - 2) * totalNationalAdditionalClassFee +
                totalNationalEachAdditionalUpTo5 +
                selectedNationalCountriesCount * 150;
            }
          }

          console.log("totalcost:", totalCost);
        } else if (q6 === "yes") {
          // WIPO Type
          if (q1 === "yes") {
            //Q1. Do you already have an international application? Yes
            //Subsequent Designation
            totalCost = 300 * CHFToGBP + 275 + totalWIPOOneClassFee; // WIPO fee with buffer
            totalCost += 350; // Our fees for one class
            if (classes > 1) {
              totalCost +=
                totamWIPOOneClassFee +
                totalWIPOSecondClassFee +
                selectedWIPOCountriesCount * 150;

              if (classes > 2) {
                totalCost +=
                  totalWIPOOneClassFee +
                  totalWIPOSecondClassFee +
                  totalWIPOThirdClassFee +
                  totalWIPOThreeClassesFee +
                  selectedWIPOCountriesCount * 150;
              }
              if (classes > 4) {
                totalCost +=
                  (classes - 2) * totalWIPOAdditionalClassFee +
                  totalWIPOEachAdditionalUpTo5 +
                  selectedWIPOCountriesCount * 150;
              }
            }
          } else if (q1 === "no") {
            // New International
            if (q3 === "yes") {
              //Q3. Do you have a UK Registration already? YES
              if (q4 === "no") {
                // Q4. Is the mark you want to protect in colour? NO
                totalCost = 653 * CHFToGBP; // WIPO fee with buffer
                totalCost += 475; // Our fees for one class
                totalCost += 40; // Filing through UK office

                if (classes > 1) {
                  totalCost +=
                    totamWIPOOneClassFee +
                    totalWIPOSecondClassFee +
                    selectedWIPOCountriesCount * 150;

                  if (classes > 2) {
                    totalCost +=
                      totalWIPOOneClassFee +
                      totalWIPOSecondClassFee +
                      totalWIPOThirdClassFee +
                      totalWIPOThreeClassesFee +
                      selectedWIPOCountriesCount * 150;
                  }
                  if (classes > 4) {
                    totalCost +=
                      (classes - 2) * totalWIPOAdditionalClassFee +
                      totalWIPOEachAdditionalUpTo5 +
                      selectedWIPOCountriesCount * 150;
                  }
                }
              } else if (q4 === "yes") {
                // Q4. Is the mark you want to protect in colour? YES
                totalCost = 903 * CHFToGBP; // WIPO fee with buffer
                totalCost += 475; // Our fees for one class
                totalCost += 40; // Filing through UK office
                if (classes > 1) {
                  totalCost +=
                    totamWIPOOneClassFee +
                    totalWIPOSecondClassFee +
                    selectedWIPOCountriesCount * 150;

                  if (classes > 2) {
                    totalCost +=
                      totalWIPOOneClassFee +
                      totalWIPOSecondClassFee +
                      totalWIPOThirdClassFee +
                      totalWIPOThreeClassesFee +
                      selectedWIPOCountriesCount * 150;
                  }
                  if (classes > 4) {
                    totalCost +=
                      (classes - 2) * totalWIPOAdditionalClassFee +
                      totalWIPOEachAdditionalUpTo5 +
                      selectedWIPOCountriesCount * 150;
                  }
                }
              }
            } else if (q3 === "no") {
              //if UK selected
              // UKIPO fees: £170 for 1 class; additional £50 per extra class.
              // Our fees: £520 for 1 class; additional £100 per extra class.
              totalCost = 170 + 520; // £170 + £520
              totalCost = 653 * CHFToGBP;
              totalCost += 475; // Our fees for one class
              totalCost += 40; // Filing through UK office
              if (classes > 1) {
                totalCost +=
                  totamWIPOOneClassFee +
                  totalWIPOSecondClassFee +
                  selectedWIPOCountriesCount * 150;

                if (classes > 2) {
                  totalCost +=
                    totalWIPOOneClassFee +
                    totalWIPOSecondClassFee +
                    totalWIPOThirdClassFee +
                    totalWIPOThreeClassesFee +
                    selectedWIPOCountriesCount * 150;
                }
                if (classes > 4) {
                  totalCost +=
                    (classes - 2) * totalWIPOAdditionalClassFee +
                    totalWIPOEachAdditionalUpTo5 +
                    selectedWIPOCountriesCount * 150;
                }
              }
            }
          }
        }

        document.getElementById(
          "worldTotalCost"
        ).textContent = `World Total Cost: £${Math.round(
          totalCost.toFixed(2)
        )}`;
      }

      //Add event listener for classesSelect dropdown

      classesSelect.addEventListener("change", calculateOtherCost);

      // Add event listeners for all radio buttons within the set of questions
      const radioButtons = document.querySelectorAll('input[type="radio"]');
      radioButtons.forEach(function (radio) {
        radio.addEventListener("change", calculateOtherCost);
      });

      // Add event listeners for WIPO and National country selections
      wipoDropdownOptions.addEventListener("change", function () {
        updateWIPOselectedCountries();
        calculateOtherCost(); // Trigger cost calculation
      });

      nationalDropdownOptions.addEventListener("change", function () {
        updateNationalselectedCountries();
        calculateOtherCost(); // Trigger cost calculation
      });
