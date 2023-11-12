1. エピソード視聴数トップ3のエピソードタイトルと視聴数を取得するクエリ:

```sql
SELECT Episodes.episode_title, ViewCounts.view_count
FROM ViewCounts
JOIN Episodes ON ViewCounts.episode_id = Episodes.id
ORDER BY ViewCounts.view_count DESC
LIMIT 3;

```

2. エピソード視聴数トップ3の番組情報とシーズン情報を含むクエリ:

```sql
SELECT Programs.program_title, Seasons.season_number, Episodes.episode_number, Episodes.episode_title, ViewCounts.view_count
FROM ViewCounts
JOIN ProgramSlots ON ViewCounts.programslot_id = ProgramSlots.id
JOIN Programs ON ProgramSlots.program_id = Programs.id
JOIN Seasons ON Programs.id = Seasons.program_id
JOIN Episodes ON Seasons.id = Episodes.season_id
ORDER BY ViewCounts.view_count DESC
LIMIT 3;

```

3. 本日の番組表を表示するためのクエリ

```sql
SELECT Channels.channel_name, ProgramSlots.start_time, ProgramSlots.end_time, Seasons.season_number, Episodes.episode_number, Episodes.episode_title, Episodes.episode_details
FROM ProgramSlots
JOIN Channels ON ProgramSlots.channel_id = Channels.id
JOIN Programs ON ProgramSlots.program_id = Programs.id
JOIN Seasons ON Programs.id = Seasons.program_id
JOIN Episodes ON Seasons.id = Episodes.season_id
WHERE DATE(ProgramSlots.start_time) = CURDATE()
ORDER BY ProgramSlots.start_time;

```

4. ドラマチャンネルの一週間分の番組表を表示するクエリ

```sql
SELECT ProgramSlots.start_time, ProgramSlots.end_time, Seasons.season_number, Episodes.episode_number, Episodes.episode_title, Episodes.episode_details
FROM ProgramSlots
JOIN Programs ON ProgramSlots.program_id = Programs.id
JOIN Seasons ON Programs.id = Seasons.program_id
JOIN Episodes ON Seasons.id = Episodes.season_id
WHERE ProgramSlots.channel_id = (SELECT id FROM Channels WHERE channel_name = 'ドラマ')
  AND ProgramSlots.start_time >= CURDATE()
  AND ProgramSlots.start_time < CURDATE() + INTERVAL 1 WEEK
ORDER BY ProgramSlots.start_time;

```

5. 直近一週間で最も見られた番組のクエリ:

```sql
SELECT Programs.program_title, SUM(ViewCounts.view_count) AS total_view_count
FROM ViewCounts
JOIN ProgramSlots ON ViewCounts.programslot_id = ProgramSlots.id
JOIN Programs ON ProgramSlots.program_id = Programs.id
WHERE ProgramSlots.start_time >= CURDATE() - INTERVAL 1 WEEK
GROUP BY Programs.program_title
ORDER BY total_view_count DESC
LIMIT 2;

```

