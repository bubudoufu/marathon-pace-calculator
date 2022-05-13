<script>
  import Button from "./lib/Button.svelte";

  let distance = "42.195";
  let time = "04:00:00";
  $: pace = timeTosce(time, distance);

  // ボタンで距離入力
  function distanceBtn(e) {
    distance = e.target.value;
  }

  // 入力された時間を秒に変換
  function timeTosce(time, distance) {
    if (!distance) {
      return "00:00:00";
    }
    let [h, m, s] = time.split(":");
    if (s === undefined) {
      s = "00";
    }
    const sec = Number(h * 3600) + Number(m * 60) + Number(s);
    return sceTotime(sec, distance);
  }

  // 秒を時間に変換
  function sceTotime(sec, distance) {
    const paceSec = sec / Number(distance);
    // 小数点切り捨てで計算
    const h = ("00" + Math.floor(paceSec / 3600)).slice(-2);
    const m = ("00" + Math.floor((paceSec % 3600) / 60)).slice(-2);
    const s = ("00" + Math.floor(paceSec % 60)).slice(-2);

    if (h === "00") {
      return `${m}:${s}`;
    } else {
      return `${h}:${m}:${s}`;
    }
  }
</script>

<main>
  <div class="tile is-ancestor">
    <div class="tile is-vertical">
      <div class="tile is-parent">
        <article class="tile is-child box">
          <p class="title is-size-5">マラソンペース計算機</p>
          <p class="subtitle is-size-6">
            ゴールタイムか距離を入力すると１キロのペースを表示します。
          </p>
        </article>
      </div>
      <div class="tile">
        <div class="tile is-parent is-vertical">
          <article class="tile is-child notification is-primary box">
            <p class="title">1キロのペース</p>
            <p class="subtitle">（分：秒）</p>
            <p class="is-size-1 has-text-centered">{pace}</p>
          </article>
          <article class="tile is-child notification is-warning box">
            <p class="title">ゴールタイム</p>
            <p class="subtitle">（時：分：秒）</p>
            <input
              class="input is-large"
              type="time"
              step="1"
              bind:value={time}
            />
          </article>
        </div>
        <div class="tile is-parent">
          <article class="tile is-child notification is-info box">
            <p class="title">距離</p>
            <p class="subtitle">（キロメートル）</p>
            <input
              class="input is-large"
              type="number"
              step="0.1"
              min="0"
              max="200"
              bind:value={distance}
            />
            <div class="content">ボタンを押しても距離を入力できます。</div>
            <div class="title">
              <div class="buttons are-small">
                <Button
                  event={"フルマラソン(42.195km)"}
                  value={"42.195"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"ハーフマラソン(21.0975km)"}
                  value={"21.0975"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"ウルトラマラソン(100km)"}
                  value={"100"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"5km"}
                  value={"5"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"10km"}
                  value={"10"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"15km"}
                  value={"15"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"20km"}
                  value={"20"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"25km"}
                  value={"25"}
                  on:click={distanceBtn}
                />
                <Button
                  event={"30km"}
                  value={"30"}
                  on:click={distanceBtn}
                />
              </div>
            </div>
          </article>
        </div>
      </div>
    </div>
  </div>
</main>

<style>
</style>
