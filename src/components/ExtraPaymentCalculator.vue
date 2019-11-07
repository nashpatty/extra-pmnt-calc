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
                        class="nav-item nav-link"
                        :class="{ active: tab === 0 }"
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
                        :class="{ active: tab === 1 }"
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
                            min="0"
                            max="10000"
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
                            min="0"
                            max="10000"
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
                    <datepicker v-model="loanCloseDate"></datepicker>
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
                            Potential Savings:
                            {{ currencyFormat(oneTimeSavings) }}
                          </li>
                          <li class="list-group-item">
                            With a one-time extra payment of:
                            {{ currencyFormat(oneTimeExtraPayment) }}
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
                            Potential Savings:
                            {{ currencyFormat(monthlySavings) }}
                          </li>
                          <li class="list-group-item">
                            With an extra monthly payment of:
                            {{ currencyFormat(monthlyExtraPayment) }}
                          </li>
                          <li class="list-group-item">
                            Loan repayment period reduced by:
                            {{ currencyFormat(100) }}
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
          <p>YOU CAN EXPECT TO SAVE:</p>
          <li class="list-group-item">
            Total savings in interest:
            {{
              tab === 0
                ? currencyFormat(oneTimeSavings)
                : currencyFormat(monthlySavings)
            }}
          </li>
          <li class="list-group-item">
            By paying an extra principal payment
          </li>
          <li v-if="tab === 0" class="list-group-item">
            One-time: {{ currencyFormat(oneTimeExtraPayment) }}
          </li>
          <li v-if="tab === 1" class="list-group-item">
            Monthly: {{ currencyFormat(monthlyExtraPayment) }}
          </li>
          <p>INFORMATION ABOUT YOUR CURRENT MORTGAGE:</p>
          <li class="list-group-item">
            Mortgage Loan Amount:
            {{ currencyFormat(mortgageLoanAmount) }}
          </li>
          <li class="list-group-item">
            Principal & Interest (P&I) Payment:
            {{ currencyFormat(monthlyPrincipalAndInterestPayment) }}
          </li>
          <li class="list-group-item">
            Interest Rate: {{ interestRatePercent }}%
          </li>
          <li class="list-group-item">Term: {{ term }}</li>
          <li class="list-group-item">
            Date loan closed: {{ loanCloseDate.toLocaleDateString("en-US") }}
          </li>
          <li class="list-group-item">
            Months since loan closed: {{ monthsSinceLoanClose }}
          </li>
          <li class="list-group-item">
            Number of payments remaining: {{ remainingPayments }} ({{
              Math.round(remainingPayments / 12)
            }}
            years)
          </li>
          <li class="list-group-item">
            Principal balance estimate (as of today):
            {{ currencyFormat(remainingPrincipalAndInterest) }}
          </li>
          <li class="list-group-item">
            Principal & interest (P&I) balance estimate:
            {{ currencyFormat(principalBalanceEstimate) }}
          </li>
          <p>
            INFORMATION ABOUT YOUR POTENTIAL MORTGAGE AFTER YOUR EXTRA PAYMENT:
          </p>
          <li v-if="tab === 0" class="list-group-item">
            One-time extra payment: {{ currencyFormat(oneTimeExtraPayment) }}
          </li>
          <li v-if="tab === 1" class="list-group-item">
            Monthly extra payment: {{ currencyFormat(monthlyExtraPayment) }}
          </li>
          <li v-if="tab === 1" class="list-group-item">
            New monthly total payment: {{ currencyFormat(newMonthlyPayment) }}
          </li>
          <li class="list-group-item">
            New number of payments remaining:
            {{ currencyFormat(remainingPayments) }}
          </li>
          <li class="list-group-item">
            New total principal & interest (P&I) remaining:
            {{
              tab === 0
                ? currencyFormat(newRemainingOneTimePrincipalAndInterest)
                : currencyFormat(newRemainingMonthlyPrincipalAndInterest)
            }}
          </li>
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
        bank, credit union, housing advisor, or lender to determine accurate
        figures.
      </p>
    </div>
  </div>
</template>


<script>
import { required, between } from "vuelidate/lib/validators";
import Datepicker from "vuejs-datepicker";

const today = new Date();
const currency = new Intl.NumberFormat("en-US", {
  maximumFractionDigits: 0,
  minimumFractionDigits: 0,
  style: "currency",
  currency: "USD"
});

export default {
  name: "PurchaseCalculator",
  components: {
    Datepicker
  },
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
  computed: {
    monthlyPrincipalAndInterestPayment() {
      return this.pmt(
        this.interestRatePercent / 100 / 12,
        this.term * 12,
        this.mortgageLoanAmount
      );
    },
    monthsSinceLoanClose() {
      const monthTo = today.getMonth();
      const yearTo = today.getFullYear();
      const monthFrom = this.loanCloseDate.getMonth();
      const yearFrom = this.loanCloseDate.getFullYear();
      const diff = monthTo - monthFrom + (yearTo - yearFrom) * 12;
      return diff < 0 ? 0 : diff;
    },
    remainingPayments() {
      return this.term * 12 - this.monthsSinceLoanClose;
    },
    remainingPrincipalAndInterest() {
      return this.monthlyPrincipalAndInterestPayment * this.remainingPayments;
    },
    principalBalanceEstimate() {
      // TODO IPMT formula
      return 10000;
    },
    newMonthlyPayment() {
      return this.monthlyPrincipalAndInterestPayment + this.monthlyExtraPayment;
    },
    newRemainingPayments() {
      // TODO NPER formula
      return 500;
    },
    newRemainingMonthlyPrincipalAndInterest() {
      return this.newMonthlyPayment * this.newRemainingPayments;
    },
    monthlySavings() {
      return (
        this.remainingPrincipalAndInterest -
        this.newRemainingMonthlyPrincipalAndInterest
      );
    },
    newRemainingOneTimePrincipalAndInterest() {
      // TODO NPER formula
      return 80000;
    },
    newPrincipalBalance() {
      return this.principalBalanceEstimate - this.oneTimeExtraPayment;
    },
    oneTimeSavings() {
      return (
        this.remainingPrincipalAndInterest -
        this.newRemainingOneTimePrincipalAndInterest
      );
    }
  },
  methods: {
    init() {
      return {
        isSubmitted: false,
        oneTimeExtraPayment: 1000,
        monthlyExtraPayment: 100,
        mortgageLoanAmount: 190000,
        loanCloseDate: new Date(),
        interestRatePercent: 4.25,
        term: 30,
        errorMsgPre: "Please enter a valid amount between",
        tab: 0
      };
    },
    reset() {
      this.oneTimeExtraPayment = this.init().oneTimeExtraPayment;
      this.monthlyExtraPayment = this.init().monthlyExtraPayment;
      this.mortgageLoanAmount = this.init().mortgageLoanAmount;
      this.interestRatePercent = this.init().interestRatePercent;
      this.loanCloseDate = this.init().loanCloseDate;
      this.term = this.init().term;
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
    currencyFormat(n) {
      return currency.format(n);
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
