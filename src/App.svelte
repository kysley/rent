<script lang="ts">
  const date = new Date();
  const today = date.getDate();
  const daysTillRent = 25 - today;

  let costOfInternet = 108.48;
  let costOfGas = 0;
  let costOfHydro = 0;

  $: utilityCosts = costOfGas + costOfInternet + costOfHydro;

  function calculateRent(costs: number) {
    const costsWithBankFees = costs + 5;
    return {
      lake: (967 + costsWithBankFees / 3).toFixed(2),
      nick: (892 + costsWithBankFees / 3).toFixed(2),
      evan: (1042 + costsWithBankFees / 3).toFixed(2),
    };
  }

  $: rents = calculateRent(utilityCosts);
</script>

<main>
  <h1>rent is due in {daysTillRent} day(s) ⌚</h1>
  <div class="form">
    <label for="gas">
      gas
      <input id="gas" type="number" bind:value={costOfGas} />
    </label>
    <label for="hydro">
      hydro
      <input id="hydro" type="number" bind:value={costOfHydro} />
    </label>
    <label for="internet">
      internet
      <input id="internet" type="number" bind:value={costOfInternet} />
    </label>
  </div>
  <div class="rents">
    <span>Evan: {rents.evan}</span>
    <span>Lake: {rents.lake}</span>
    <span>Nick: {rents.nick}</span>
  </div>
  <p style="font-style: italic;">
    utilites were {utilityCosts} this month. plus an extra $5 in bank fees
  </p>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }

  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: auto;
  }

  .form {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 1.4rem;
    margin: 1rem 0;
  }

  .form label {
    display: flex;
    justify-content: space-between;
    width: 100%;
    gap: 1rem;
  }

  .rents {
    display: flex;
    flex-direction: column;
    gap: 0.45rem;
  }

  h1 {
    font-size: 2rem;
    line-height: 1.1;
  }
</style>
