<template>
  <div class="sliders">
    <div v-if="!isSubmitted" id="sliders-page">
      <div class="col">
        <div class="row">
          <div class="col">
            <p>
              See how an extra mortgage payment may save money and shorten the
              time it takes to pay off your loan.
            </p>
            <p class="text-italic">
              Note: Calculators display default values. Enter new figures to
              override.
            </p>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <form action>
              <div class="row">
                <div id="input" class="col col-md-6">
                  <nav>
                    <div
                      id="results-nav-tab"
                      class="nav nav-tabs"
                      role="tablist"
                    >
                      <a
                        @click="tab = 0"
                        id="nav-one-time-info-tab"
                        class="nav-item nav-link active"
                        data-toggle="tab"
                        href="#nav-one-time-info"
                        role="tab"
                        aria-controls="nav-one-time-info"
                        aria-selected="true"
                        >One-Time</a
                      >
                      <a
                        @click="tab = 1"
                        id="nav-monthly-info-tab"
                        class="nav-item nav-link"
                        data-toggle="tab"
                        href="#nav-monthly-info"
                        role="tab"
                        aria-controls="nav-monthly-info"
                        aria-selected="false"
                        >Monthly</a
                      >
                    </div>
                  </nav>
                  <div id="nav-tabContent" class="tab-content">
                    <div
                      id="nav-one-time-info"
                      class="tab-pane show active"
                      role="tabpanel"
                      aria-labelledby="nav-one-time-info-tab"
                    >
                      <div id="gross-income-input-group" class="form-group">
                        <label for="gross-income-input-field"
                          >Extra Payment: One-Time</label
                        >
                        <div class="input-group mb-2">
                          <div class="input-group-prepend">
                            <div class="input-group-text">$</div>
                          </div>
                          <input
                            id="gross-income-input-field"
                            v-model.number="$v.oneTimeExtraPayment.$model"
                            type="number"
                            class="form-control"
                            :class="{
                              'is-invalid':
                                $v.oneTimeExtraPayment.$error ||
                                $v.oneTimeExtraPayment.$invalid
                            }"
                          />
                          <input
                            id="gross-income-input-range"
                            v-model.number="oneTimeExtraPayment"
                            type="range"
                            class="custom-range"
                            min="10000"
                            max="1000000"
                          />
                          <div class="invalid-feedback">
                            <span
                              v-if="
                                !$v.oneTimeExtraPayment.between ||
                                  !$v.oneTimeExtraPayment.required
                              "
                              >{{ errorMsgPre }} ${{
                                Number(
                                  $v.oneTimeExtraPayment.$params.between.min
                                ).toLocaleString()
                              }}
                              and ${{
                                Number(
                                  $v.oneTimeExtraPayment.$params.between.max
                                ).toLocaleString()
                              }}</span
                            >
                          </div>
                        </div>
                      </div>
                    </div>
                    <div
                      id="nav-monthly-info"
                      class="tab-pane"
                      role="tabpanel"
                      aria-labelledby="nav-monthly-info-tab"
                    >
                      <div id="gross-income-input-group" class="form-group">
                        <label for="gross-income-input-field"
                          >Extra Payment: Monthly</label
                        >
                        <div class="input-group mb-2">
                          <div class="input-group-prepend">
                            <div class="input-group-text">$</div>
                          </div>
                          <input
                            id="gross-income-input-field"
                            v-model.number="$v.monthlyExtraPayment.$model"
                            type="number"
                            class="form-control"
                            :class="{
                              'is-invalid':
                                $v.monthlyExtraPayment.$error ||
                                $v.monthlyExtraPayment.$invalid
                            }"
                          />
                          <div class="input-group-append">
                            <div class="input-group-text">mo</div>
                          </div>
                          <input
                            id="gross-income-input-range"
                            v-model.number="monthlyExtraPayment"
                            type="range"
                            class="custom-range"
                            min="10000"
                            max="1000000"
                          />
                          <div class="invalid-feedback">
                            <span
                              v-if="
                                !$v.monthlyExtraPayment.between ||
                                  !$v.monthlyExtraPayment.required
                              "
                              >{{ errorMsgPre }} ${{
                                Number(
                                  $v.monthlyExtraPayment.$params.between.min
                                ).toLocaleString()
                              }}
                              and ${{
                                Number(
                                  $v.monthlyExtraPayment.$params.between.max
                                ).toLocaleString()
                              }}</span
                            >
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div id="gross-income-input-group" class="form-group">
                    <label for="gross-income-input-field"
                      >Mortgage Loan Amount</label
                    >
                    <div class="input-group mb-2">
                      <div class="input-group-prepend">
                        <div class="input-group-text">$</div>
                      </div>
                      <input
                        id="gross-income-input-field"
                        v-model.number="$v.mortgageLoanAmount.$model"
                        type="number"
                        class="form-control"
                        :class="{
                          'is-invalid':
                            $v.mortgageLoanAmount.$error ||
                            $v.mortgageLoanAmount.$invalid
                        }"
                      />
                      <input
                        id="gross-income-input-range"
                        v-model.number="mortgageLoanAmount"
                        type="range"
                        class="custom-range"
                        min="10000"
                        max="1000000"
                      />
                      <div class="invalid-feedback">
                        <span
                          v-if="
                            !$v.mortgageLoanAmount.between ||
                              !$v.mortgageLoanAmount.required
                          "
                          >{{ errorMsgPre }} ${{
                            Number(
                              $v.mortgageLoanAmount.$params.between.min
                            ).toLocaleString()
                          }}
                          and ${{
                            Number(
                              $v.mortgageLoanAmount.$params.between.max
                            ).toLocaleString()
                          }}</span
                        >
                      </div>
                    </div>
                  </div>
                  <div id="term-input-group" class="form-group">
                    <label for="term-input-select">Term</label>
                    <div class="input-group mb-2">
                      <select
                        id="term-input-select"
                        v-model.number="term"
                        class="form-control"
                      >
                        <option>10</option>
                        <option>15</option>
                        <option>20</option>
                        <option>25</option>
                        <option selected>30</option>
                      </select>
                      <div class="input-group-append">
                        <div class="input-group-text">yrs</div>
                      </div>
                      <input
                        id="term-input-range"
                        v-model.number="term"
                        type="range"
                        class="custom-range"
                        min="10"
                        max="30"
                        step="5"
                      />
                    </div>
                  </div>
                  <div id="interest-rate-input-group" class="form-group">
                    <label for="interest-rate-input-field">Interest Rate</label>
                    <div class="input-group mb-2">
                      <input
                        id="interest-rate-input-field"
                        v-model.number="$v.interestRatePercent.$model"
                        type="number"
                        step="0.25"
                        class="form-control"
                        :class="{
                          'is-invalid':
                            $v.interestRatePercent.$error ||
                            $v.interestRatePercent.$invalid
                        }"
                      />
                      <div class="input-group-append">
                        <div class="input-group-text">%</div>
                      </div>
                      <input
                        id="interest-rate-input-range"
                        v-model.number="interestRatePercent"
                        type="range"
                        class="custom-range"
                        min="2.5"
                        max="11"
                        step="0.25"
                      />
                      <div class="invalid-feedback">
                        <span
                          v-if="
                            !$v.interestRatePercent.between ||
                              !$v.interestRatePercent.required
                          "
                          >{{ errorMsgPre }}
                          {{
                            Number(
                              $v.interestRatePercent.$params.between.min
                            ).toLocaleString()
                          }}% and
                          {{
                            Number(
                              $v.interestRatePercent.$params.between.max
                            ).toLocaleString()
                          }}%</span
                        >
                      </div>
                    </div>
                  </div>
                  <div id="gross-income-input-group" class="form-group">
                    <label for="gross-income-input-field"
                      >Date Loan Closed</label
                    >
                    <div class="input-group mb-2">
                      <div class="input-group-prepend">
                        <div class="input-group-text">$</div>
                      </div>
                      <input
                        id="gross-income-input-field"
                        v-model.number="$v.mortgageLoanAmount.$model"
                        type="number"
                        class="form-control"
                        :class="{
                          'is-invalid':
                            $v.mortgageLoanAmount.$error ||
                            $v.mortgageLoanAmount.$invalid
                        }"
                      />
                      <input
                        id="gross-income-input-range"
                        v-model.number="mortgageLoanAmount"
                        type="range"
                        class="custom-range"
                        min="10000"
                        max="1000000"
                      />
                      <div class="invalid-feedback">
                        <span
                          v-if="
                            !$v.mortgageLoanAmount.between ||
                              !$v.mortgageLoanAmount.required
                          "
                          >{{ errorMsgPre }} ${{
                            Number(
                              $v.mortgageLoanAmount.$params.between.min
                            ).toLocaleString()
                          }}
                          and ${{
                            Number(
                              $v.mortgageLoanAmount.$params.between.max
                            ).toLocaleString()
                          }}</span
                        >
                      </div>
                    </div>
                  </div>
                </div>
                <div id="result" class="col col-md-6">
                  <div class="sticky">
                    <nav>
                      <div
                        id="results-nav-tab"
                        class="nav nav-tabs"
                        role="tablist"
                      >
                        <a
                          id="nav-potential-saving-tab"
                          class="nav-item nav-link active"
                          data-toggle="tab"
                          href="#nav-potential-savings"
                          role="tab"
                          aria-controls="nav-potential-saving"
                          aria-selected="true"
                          >Potential Savings</a
                        >
                      </div>
                    </nav>
                    <div id="nav-tabContent" class="tab-content">
                      <div
                        v-if="tab === 0"
                        id="nav-one-time-result"
                        class="tab-pane fade show active"
                        role="tabpanel"
                        aria-labelledby="nav-one-time-result"
                      >
                        <ul class="list-group">
                          <li class="list-group-item">
                            One Time Mortgage Payment: ${{
                              Math.round(totalMonthlyMortgage)
                            }}
                          </li>
                          <li class="list-group-item">
                            PMI: ${{ Math.round(monthlyMortgageInsurance) }}
                          </li>
                          <li class="list-group-item">
                            HOA: ${{ Math.round(hoa) }}
                          </li>
                          <li class="list-group-item">
                            Taxes & Insurance: ${{
                              Math.round(monthlyPropertyTax + monthlyHoi)
                            }}
                          </li>
                          <li class="list-group-item">
                            Principal & Interest: ${{
                              Math.round(monthlyPrincipalInterestPayment)
                            }}
                          </li>
                        </ul>
                      </div>
                      <div
                        v-if="tab === 1"
                        id="nav-monthly-result"
                        class="tab-pane fade show active"
                        role="tabpanel"
                        aria-labelledby="nav-monthly-result"
                      >
                        <ul class="list-group">
                          <li class="list-group-item">
                            Monthly Mortgage Payment: ${{
                              Math.round(totalMonthlyMortgage)
                            }}
                          </li>
                          <li class="list-group-item">
                            PMI: ${{ Math.round(monthlyMortgageInsurance) }}
                          </li>
                          <li class="list-group-item">
                            HOA: ${{ Math.round(hoa) }}
                          </li>
                          <li class="list-group-item">
                            Taxes & Insurance: ${{
                              Math.round(monthlyPropertyTax + monthlyHoi)
                            }}
                          </li>
                          <li class="list-group-item">
                            Principal & Interest: ${{
                              Math.round(monthlyPrincipalInterestPayment)
                            }}
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="col">
                  <hr />
                  <div class="row">
                    <div id="form-mod-group" class="form-group col col-md-6">
                      <button type="button" class="btn btn-base" @click="reset">
                        Reset
                      </button>
                    </div>
                    <div id="submit-form-group" class="form-group col col-md-6">
                      <button
                        class="btn btn-block resultsBtn btn-primary"
                        type="submit"
                        :disabled="$v.$invalid"
                        @click.prevent="isSubmitted = !isSubmitted"
                      >
                        See Results <i class="fa fa-caret-right" />
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
    <div v-if="isSubmitted" id="result-page">
      <div class="col">
        <ul class="list-group">
          <p>YOU CAN EXPECT TO PAY:</p>
          <li class="list-group-item">
            Home Purchase Price: ${{ Math.round(homePurchasePrice) }}
          </li>
          <li class="list-group-item">
            Mortgage Loan Amount: ${{ Math.round(mortgageLoanAmount) }}
          </li>
          <li class="list-group-item">
            Total Mortgage Payment: ${{ Math.round(totalMonthlyMortgage) }}
          </li>
          <p>EXPECTED FUNDS NEEDED AT CLOSING:</p>
          <li class="list-group-item">
            Total Cash Required: ${{ Math.round(downPayment + closingCost) }}
          </li>
          <li class="list-group-item">
            Down Payment: ${{ Math.round(downPayment) }}
          </li>
          <li class="list-group-item">
            Closing Costs: ${{ Math.round(closingCost) }}
          </li>
          <p>INFORMATION ABOUT YOUR POTENTIAL MORTGAGE:</p>
          <li class="list-group-item">
            Mortgage Loan Amount: ${{ Math.round(mortgageLoanAmount) }}
          </li>
          <li class="list-group-item">Term: ${{ Math.round(term) }}</li>
          <li class="list-group-item">
            Total Mortgage Payment: ${{ Math.round(totalMonthlyMortgage) }}
          </li>
          <li class="list-group-item">
            Principal & Interest (P&I) Payment: ${{
              Math.round(monthlyPrincipalInterestPayment)
            }}
          </li>
          <li class="list-group-item">
            Property Taxes: ${{ Math.round(monthlyPropertyTax) }}
          </li>
          <li class="list-group-item">
            Homeowners Insurance: ${{ Math.round(monthlyHoi) }}
          </li>
          <li class="list-group-item">
            PMI: ${{ Math.round(monthlyMortgageInsurance) }}
          </li>
          <li class="list-group-item">HOA Fees: ${{ Math.round(hoa) }}</li>
          <li class="list-group-item">LTV: ${{ Math.round(ltv) }}</li>
        </ul>
      </div>
      <button
        class="btn btn-block btn-primary"
        @click.prevent="isSubmitted = !isSubmitted"
      >
        Back to Calculator &#8677;
      </button>
      <p>
        These calculator results are estimates based on your inputs. Contact a
        bank, credit union, housing advisor, or lender to determine your loan
        eligibility and accurate costs. Fannie Mae does not offer mortgage loans
        to consumers and this in no way indicates approval or financing of a
        mortgage loan.
      </p>
    </div>
  </div>
</template>


<script>
import { required, between } from "vuelidate/lib/validators";

export default {
  name: "PurchaseCalculator",
  data() {
    return this.init();
  },
  validations: {
    oneTimeExtraPayment: {
      required,
      between: between(0, 10000)
    },
    monthlyExtraPayment: {
      required,
      between: between(0, 10000)
    },
    mortgageLoanAmount: {
      required,
      between: between(10000, 1000000)
    },
    interestRatePercent: {
      required,
      between: between(2.5, 11)
    }
  },
  computed: {},
  methods: {
    init() {
      return {
        isSubmitted: false,
        oneTimeExtraPayment: 1000,
        monthlyExtraPayment: 100,
        mortgageLoanAmount: 190000,
        dateLoanClosed: 190000,
        interestRatePercent: 4.25,
        term: 30,
        errorMsgPre: "Please enter a valid amount between",
        tab: 0
      };
    },
    reset() {
      this.homePurchasePrice = this.init().homePurchasePrice;
      this.downPaymentPercent = this.init().downPaymentPercent;
      this.interestRatePercent = this.init().interestRatePercent;
      this.term = this.init().term;
      this.hoi = this.init().hoi;
      this.hoa = this.init().hoa;
      this.propertyTax = this.init().propertyTax;
    },
    pmt(rate, period, pv) {
      return (pv * rate) / (1 - (1 + rate) ** (-1 * period));
    },
    handleNegativeNums(n) {
      if (n < 0) {
        return 0;
      }
      return n;
    },
    updateFees() {
      let dynamicHoa = Math.round((this.homePurchasePrice * 0.0025) / 12);
      this.hoa =
        dynamicHoa > this.$v.hoa.$params.between.max
          ? this.$v.hoa.$params.between.max
          : dynamicHoa;
      let dynamicHoi = Math.round(this.homePurchasePrice * 0.0075);
      this.hoi =
        dynamicHoi > this.$v.hoi.$params.between.max
          ? this.$v.hoi.$params.between.max
          : dynamicHoi;
      let dynamicTax = Math.round(this.homePurchasePrice * 0.0125);
      this.propertyTax =
        dynamicTax < this.$v.propertyTax.$params.between.min
          ? this.$v.propertyTax.$params.between.min
          : dynamicTax;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.sticky {
  position: -webkit-sticky;
  position: sticky;
  top: 0;
}
.background-lightblue {
  background-color: lightblue;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
