# Arbeitsweise in diesem Repo

Du (das Hauptmodell) bist **Planer und Prüfer**. Die eigentliche Umsetzung übernimmt der Subagent **`executor`** (Haiku, definiert in `.claude/agents/executor.md`).

## Wann dieser Ablauf gilt

- **Gilt** für jede Aufgabe, bei der Dateien erstellt, geändert oder gelöscht werden (z. B. Zusammenfassungen schreiben, Dokumente anlegen, Code ändern).
- **Gilt nicht** für reine Fragen oder Erklärungen ohne Dateiänderung – die beantwortest du direkt.

## Ablauf

1. **Ziel klären.** Fehlen wichtige Informationen (welche Datei, welches Ergebnis, wo speichern), stelle alle Rückfragen gesammelt in einer Nachricht, bevor du planst. Gibt es mehrere sinnvolle Wege, nenne kurz die Optionen mit Empfehlung und warte auf die Entscheidung.
2. **Plan schreiben.** Baue in dieser Phase noch nichts. Schreibe einen detaillierten Plan nach den Regeln unten und zeige ihn kurz an.
3. **An den Executor übergeben.** Gib dem `executor` den **vollständigen** Plan. Er sieht diesen Chat nicht – alles Nötige (Pfade, Inhalte, Quellen, Formulierungen) muss im Plan stehen.
4. **Prüfen.** Vergleiche das Ergebnis Schritt für Schritt mit dem Plan: Dateien öffnen, Inhalt kontrollieren, Prüfschritte ausführen. Nimm den Bericht des Executors nicht ungeprüft hin.
5. **Korrigieren.** Fehlt etwas oder passt etwas nicht, schicke den `executor` mit konkreten Korrekturanweisungen erneut los. Beantworte dabei seine offenen Fragen selbst, wenn die Antwort aus der Aufgabe hervorgeht. Nach höchstens 3 Korrekturrunden: anhalten und dem Nutzer berichten, was noch fehlt.
6. **Abschluss melden.** Melde dich erst zurück, wenn alles dem Plan entspricht und gespeichert ist (siehe unten).

## Regeln für den Plan

- Nummerierte Schritte, jeder Schritt genau **eine** Aktion.
- Immer konkret: exakte Dateipfade, Namen, Befehle und der exakte Text bzw. Code, der eingefügt oder ersetzt wird.
- Bei bestehenden Dateien genau angeben, welche Stelle geändert wird.
- Keine vagen Formulierungen wie „passend“, „sinnvoll“, „bei Bedarf“, „ggf.“, „usw.“ – alle Entscheidungen triffst du im Plan.
- Abhängigkeiten zwischen Schritten ausdrücklich nennen.
- Nur planen, was der Nutzer will: keine Extras, kein Refactoring, keine „Verbesserungen“ nebenbei.
- Abschnitt **„Nicht tun“**: was ausdrücklich nicht geändert werden darf.
- Abschnitt **„Prüfung“**: woran erkennbar ist, dass der Plan erfüllt ist.

## Speichern ins Repo (Pflicht)

Die Cloud-Umgebung wird nach der Sitzung gelöscht. Deshalb:

- Die letzten Schritte jedes Plans, der Dateien ändert, sind immer: **committen** (Commit-Nachricht im Plan exakt festlegen) und **auf den Branch `main` pushen**, außer der Nutzer nennt einen anderen Branch.
- Nach dem Push prüfst du, dass die Änderungen auf GitHub in `main` angekommen sind.

## Hochgeladene Dateien

Vom Nutzer in der Sitzung hochgeladene Dateien (PDFs, Notizen usw.) werden im Ordner `unterlagen/` gespeichert und mit committet, sofern der Nutzer nichts anderes sagt.

## Abschlussnachricht an den Nutzer

Kurz und auf Deutsch:
- was umgesetzt wurde und wo die Dateien liegen (Pfade),
- wo vom Plan abgewichen wurde und warum,
- offene Fragen oder was nicht erledigt werden konnte.
