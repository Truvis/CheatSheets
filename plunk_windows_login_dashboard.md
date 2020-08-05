<form theme="dark">
  <label>Windows Login</label>
  <fieldset submitButton="true" autoRun="false">
    <input type="text" token="filter1" searchWhenChanged="true">
      <label>Filter:</label>
      <default>*</default>
    </input>
  </fieldset>
  <row>
    <panel>
      <title>Failed Login Events</title>
      <input type="time" token="time1" searchWhenChanged="true">
        <label></label>
        <default>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </default>
      </input>
      <input type="multiselect" token="multi_select1" searchWhenChanged="true">
        <label>Field Section:</label>
        <choice value="_time">_time</choice>
        <choice value="host">host</choice>
        <choice value="user">user</choice>
        <choice value="src_ip">src_ip</choice>
        <choice value="EventCode">EventCode</choice>
        <choice value="signature">signature</choice>
        <choice value="Logon_Type">Logon_Type</choice>
        <choice value="Logon_Process">Logon_Process</choice>
        <default>user</default>
        <delimiter>, </delimiter>
      </input>
      <table>
        <search>
          <query>source="WinEventLog:Security" $filter1$ TaskCategory=Logon Keywords="Audit Failure" | fillnull value=* src_ip EventCode | stats count by $multi_select1$ 
| sort -count</query>
          <earliest>$time1.earliest$</earliest>
          <latest>$time1.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="count">10</option>
        <option name="dataOverlayMode">none</option>
        <option name="drilldown">none</option>
        <option name="percentagesRow">false</option>
        <option name="refresh.display">progressbar</option>
        <option name="rowNumbers">false</option>
        <option name="totalsRow">false</option>
        <option name="wrap">true</option>
      </table>
    </panel>
    <panel>
      <title>Successful Login Events</title>
      <input type="time" token="time2" searchWhenChanged="true">
        <label></label>
        <default>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </default>
      </input>
      <input type="multiselect" token="multi_select2" searchWhenChanged="true">
        <label>Field Section:</label>
        <choice value="_time">_time</choice>
        <choice value="host">host</choice>
        <choice value="user">user</choice>
        <choice value="src_ip">src_ip</choice>
        <choice value="EventCode">EventCode</choice>
        <choice value="signature">signature</choice>
        <choice value="Logon_Type">Logon_Type</choice>
        <choice value="Logon_Process">Logon_Process</choice>
        <choice value="Process_Name">Process_Name</choice>
        <default>user</default>
        <delimiter>, </delimiter>
      </input>
      <table>
        <search>
          <query>source="WinEventLog:Security" $filter1$ TaskCategory=Logon Keywords="Audit Success" user!="DWM-*" user!="UMFD-*" user!=SYSTEM user!="LOCAL SERVICE" user!="NETWORK SERVICE" user!="*$$" user!="ANONYMOUS LOGON" user!="IUSR" | fillnull value=* src_ip EventCode Logon_Type, Logon_Process, Process_Name | stats count by $multi_select2$ 
| sort -count</query>
          <earliest>$time2.earliest$</earliest>
          <latest>$time2.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="count">10</option>
        <option name="dataOverlayMode">none</option>
        <option name="drilldown">none</option>
        <option name="percentagesRow">false</option>
        <option name="refresh.display">progressbar</option>
        <option name="rowNumbers">false</option>
        <option name="totalsRow">false</option>
        <option name="wrap">true</option>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <title>Privileged Account Events</title>
      <input type="time" token="time3" searchWhenChanged="true">
        <label></label>
        <default>
          <earliest>-24h@h</earliest>
          <latest>now</latest>
        </default>
      </input>
      <input type="multiselect" token="multi_select3" searchWhenChanged="true">
        <label>Field Section:</label>
        <choice value="_time">_time</choice>
        <choice value="host">host</choice>
        <choice value="user">user</choice>
        <choice value="signature">signature</choice>
        <choice value="vendor_privilege">vendor_privilege</choice>
        <choice value="member_id">member_id</choice>
        <choice value="Keywords">Keywords</choice>
        <default>user</default>
        <delimiter>, </delimiter>
      </input>
      <table>
        <search>
          <query>source="WinEventLog:Security" $filter1$ TaskCategory="Special Logon" user!="DWM-*" user!="UMFD-*" user!=SYSTEM user!="LOCAL SERVICE" user!="NETWORK SERVICE" user!="*$" user!="ANONYMOUS LOGON" user!="IUSR" | stats count by $multi_select3$ | sort -count</query>
          <earliest>$time3.earliest$</earliest>
          <latest>$time3.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="count">20</option>
        <option name="dataOverlayMode">none</option>
        <option name="drilldown">none</option>
        <option name="percentagesRow">false</option>
        <option name="refresh.display">progressbar</option>
        <option name="rowNumbers">false</option>
        <option name="totalsRow">false</option>
        <option name="wrap">true</option>
      </table>
    </panel>
  </row>
</form>
