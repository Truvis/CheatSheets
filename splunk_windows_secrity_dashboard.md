<form theme="dark">
  <label>Windows Security Dashboard</label>
  <fieldset submitButton="false">
    <input type="time" token="timepicker">
      <label></label>
      <default>
        <earliest>-7d@h</earliest>
        <latest>now</latest>
      </default>
    </input>
  </fieldset>
  <row>
    <panel>
      <title>Failed Logon Attempts</title>
      <table>
        <search>
          <query>source="WinEventLog:security" EventCode=4625 
| eval hammer=_time
| eval Workstation_Name=lower(Workstation_Name)
| eval host=lower(host)
| bucket span=5m hammer 
| stats count sparkline by user host, hammer, Workstation_Name
| rename hammer as "5 minute blocks" host as "Target Host" Workstation_Name as "Source Host"
| convert ctime("5 minute blocks")</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
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
        <format type="color" field="user">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
        <format type="color" field="Target Host">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
        <format type="color" field="Source Host">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <title>Timechart of Failed Attempts to Logon</title>
      <chart>
        <search>
          <query>source="WinEventLog:security" EventCode=4625 
| timechart span=1h count by host</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="charting.axisLabelsX.majorLabelStyle.overflowMode">ellipsisNone</option>
        <option name="charting.axisLabelsX.majorLabelStyle.rotation">0</option>
        <option name="charting.axisTitleX.visibility">visible</option>
        <option name="charting.axisTitleY.visibility">visible</option>
        <option name="charting.axisTitleY2.visibility">visible</option>
        <option name="charting.axisX.abbreviation">none</option>
        <option name="charting.axisX.scale">linear</option>
        <option name="charting.axisY.abbreviation">none</option>
        <option name="charting.axisY.scale">linear</option>
        <option name="charting.axisY2.abbreviation">none</option>
        <option name="charting.axisY2.enabled">0</option>
        <option name="charting.axisY2.scale">inherit</option>
        <option name="charting.chart">line</option>
        <option name="charting.chart.bubbleMaximumSize">50</option>
        <option name="charting.chart.bubbleMinimumSize">10</option>
        <option name="charting.chart.bubbleSizeBy">area</option>
        <option name="charting.chart.nullValueMode">gaps</option>
        <option name="charting.chart.showDataLabels">none</option>
        <option name="charting.chart.sliceCollapsingThreshold">0.01</option>
        <option name="charting.chart.stackMode">default</option>
        <option name="charting.chart.style">shiny</option>
        <option name="charting.drilldown">none</option>
        <option name="charting.layout.splitSeries">0</option>
        <option name="charting.layout.splitSeries.allowIndependentYRanges">0</option>
        <option name="charting.legend.labelStyle.overflowMode">ellipsisMiddle</option>
        <option name="charting.legend.mode">standard</option>
        <option name="charting.legend.placement">right</option>
        <option name="charting.lineWidth">2</option>
        <option name="refresh.display">progressbar</option>
        <option name="trellis.enabled">0</option>
        <option name="trellis.scales.shared">1</option>
        <option name="trellis.size">medium</option>
      </chart>
    </panel>
  </row>
  <row>
    <panel>
      <title>Successful Logons</title>
      <table>
        <search>
          <query>source="WinEventLog:security" EventCode=4624 (Logon_Type=2 OR Logon_Type=7 OR Logon_Type=10 OR Logon_Type=11) user!="DWM-*" user!="UMFD-*"
| eval Workstation_Name=lower(Workstation_Name)
| eval host=lower(host)
| eval hammer=_time 
| bucket span=1d@d hammer 
| stats values(Logon_Type) as "Logon Type" count sparkline by user host, hammer, Workstation_Name
| rename hammer as "Start of Day" host as "Target Host" Workstation_Name as "Source Host"
| convert ctime("Start of Day")
| sort - "Start of Day"</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="count">10</option>
        <option name="drilldown">none</option>
        <option name="refresh.display">progressbar</option>
        <format type="color" field="Target Host">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
        <format type="color" field="Source Host">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
        <format type="color" field="user">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
      </table>
    </panel>
    <panel>
      <title>Timechart of Successful Logons</title>
      <chart>
        <search>
          <query>source="WinEventLog:security" EventCode=4624 (Logon_Type=2 OR Logon_Type=7 OR Logon_Type=10 OR Logon_Type=11) user!="DWM-*" user!="UMFD-*"
| timechart span=1h count by host</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="charting.axisLabelsX.majorLabelStyle.overflowMode">ellipsisNone</option>
        <option name="charting.axisLabelsX.majorLabelStyle.rotation">0</option>
        <option name="charting.axisTitleX.visibility">visible</option>
        <option name="charting.axisTitleY.visibility">visible</option>
        <option name="charting.axisTitleY2.visibility">visible</option>
        <option name="charting.axisX.abbreviation">none</option>
        <option name="charting.axisX.scale">linear</option>
        <option name="charting.axisY.abbreviation">none</option>
        <option name="charting.axisY.scale">linear</option>
        <option name="charting.axisY2.abbreviation">none</option>
        <option name="charting.axisY2.enabled">0</option>
        <option name="charting.axisY2.scale">inherit</option>
        <option name="charting.chart">line</option>
        <option name="charting.chart.bubbleMaximumSize">50</option>
        <option name="charting.chart.bubbleMinimumSize">10</option>
        <option name="charting.chart.bubbleSizeBy">area</option>
        <option name="charting.chart.nullValueMode">gaps</option>
        <option name="charting.chart.showDataLabels">none</option>
        <option name="charting.chart.sliceCollapsingThreshold">0.01</option>
        <option name="charting.chart.stackMode">default</option>
        <option name="charting.chart.style">shiny</option>
        <option name="charting.drilldown">none</option>
        <option name="charting.layout.splitSeries">0</option>
        <option name="charting.layout.splitSeries.allowIndependentYRanges">0</option>
        <option name="charting.legend.labelStyle.overflowMode">ellipsisMiddle</option>
        <option name="charting.legend.mode">standard</option>
        <option name="charting.legend.placement">right</option>
        <option name="charting.lineWidth">2</option>
        <option name="trellis.enabled">0</option>
        <option name="trellis.scales.shared">1</option>
        <option name="trellis.size">medium</option>
      </chart>
    </panel>
  </row>
  <row>
    <panel>
      <title>Windows Authentication events</title>
      <table>
        <search>
          <query>source="wineventlog:security" action=success (EventCode=4624 OR EventCode=4634 ) user!="anonymous logon" user!="DWM-*" user!="UMFD-*" user!=SYSTEM user!=*$ (Logon_Type=2 OR Logon_Type=7 OR Logon_Type=10)
| convert timeformat="%a %B %d %Y" ctime(_time) AS Date 
| streamstats earliest(_time) AS login, latest(_time) AS logout by Date, host, user
| eval session_duration=logout-login
| where session_duration &gt; 5
| eval h=floor(session_duration/3600) 
| eval m=floor((session_duration-(h*3600))/60) 
| eval SessionDuration=h."h ".m."m " 
| convert timeformat=" %m/%d/%y - %I:%M %P" ctime(login) AS login 
| convert timeformat=" %m/%d/%y - %I:%M %P" ctime(logout) AS logout 
| stats count AS auth_event_count, earliest(login) as login, max(SessionDuration) AS sesion_duration, latest(logout) as logout, values(Logon_Type) AS logon_types by Date, host, user
| sort + login</query>
          <earliest>$timepicker.earliest$</earliest>
          <latest>$timepicker.latest$</latest>
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
        <format type="color" field="host">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
        <format type="color" field="user">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
      </table>
    </panel>
  </row>
  <row>
    <panel>
      <title>Common Event Codes - 10,000 foot view</title>
      <table>
        <search>
          <query>source="wineventlog:security" user!="DWM-*" user!="UMFD-*" user!=SYSTEM user!="LOCAL SERVICE" user!="NETWORK SERVICE" user!="*$$" user!="ANONYMOUS LOGON" user!="IUSR"
| eval Trigger=case(EventCode=516, "Audit Logs Modified",EventCode=517, "Audit Logs Modified",EventCode=612, "Audit Logs Modified",EventCode=623, "Audit Logs Modified",EventCode=806, "Audit Logs Modified",EventCode=807, "Audit Logs Modified",EventCode=1101, "Audit Logs Modified",EventCode=1102, "Audit Logs Modified",EventCode=4612, "Audit Logs Modified",EventCode=4621, "Audit Logs Modified",EventCode=4694, "Audit Logs Modified",EventCode=4695, "Audit Logs Modified",EventCode=4715, "Audit Logs Modified",EventCode=4719, "Audit Logs Modified",EventCode=4817, "Audit Logs Modified",EventCode=4885, "Audit Logs Modified",EventCode=4902, "Audit Logs Modified",EventCode=4906, "Audit Logs Modified",EventCode=4907, "Audit Logs Modified",EventCode=4912, "Audit Logs Modified", EventCode=642, "Account Modification",EventCode=646, "Account Modification",EventCode=685, "Account Modification",EventCode=4738, "Account Modification",EventCode=4742, "Account Modification",EventCode=4781, "Account Modification", EventCode=1102, "Audit Logs Cleared/Deleted",EventCode=517, "Audit Logs Cleared/Deleted", EventCode=628, "Passwords Changed",EventCode=627, "Passwords Changed",EventCode=4723, "Passwords Changed",EventCode=4724, "Passwords Changed", EventCode=528, "Successful Logons",EventCode=540, "Successful Logons",EventCode=4624, "Successful Logons", EventCode=4625, "Failed Logons",EventCode=529, "Failed Logons",EventCode=530, "Failed Logons",EventCode=531, "Failed Logons",EventCode=532, "Failed Logons",EventCode=533, "Failed Logons",EventCode=534, "Failed Logons",EventCode=535, "Failed Logons",EventCode=536, "Failed Logons",EventCode=537, "Failed Logons",EventCode=539, "Failed Logons", EventCode=576, "Escalation of Privileges",EventCode=4672, "Escalation of Privileges",EventCode=577, "Escalation of Privileges",EventCode=4673, "Escalation of Privileges",EventCode=578, "Escalation of Privileges",EventCode=4674, "Escalation of Privileges") 
| stats earliest(_time) as Initial_Occurrence latest(_time) as Latest_Occurrence values(user) as Users values(host) as Hosts count sparkline by Trigger
| sort - count
| convert ctime(Initial_Occurrence) ctime(Latest_Occurrence)</query>
          <earliest>-7d@h</earliest>
          <latest>now</latest>
          <sampleRatio>1</sampleRatio>
        </search>
        <option name="count">20</option>
        <option name="dataOverlayMode">none</option>
        <option name="drilldown">none</option>
        <option name="percentagesRow">false</option>
        <option name="rowNumbers">false</option>
        <option name="totalsRow">false</option>
        <option name="wrap">true</option>
        <format type="color" field="Trigger">
          <colorPalette type="sharedList"></colorPalette>
          <scale type="sharedCategory"></scale>
        </format>
      </table>
    </panel>
  </row>
</form>
