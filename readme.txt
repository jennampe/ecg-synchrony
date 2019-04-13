### REQUIRED FILE FORMAT
See attached file example. Specifically, the csv must:
-have a throwaway first line (default BIOPAC .acq output is "Event Summary"
-headers on second line, as: "Index", "Time", "Type", "Channel"
---"Index": sequential integer numbering
---"Time:" time in seconds, with " sec" after numeric value
---"Type": event types
-----"QRS Peak" for QRS event
-----"Waveform Onset" for events serving as markers for different relevant timepoints during recording of physio (i.e. onset of manipulation, etc.)
-----"Append" for BIOPAC starter time segment
---"Channel": channel name, unique between dyadic partners

### RATER VALUE COMPARISON OUTPUT
The "gold standard rater" paradigm involves two raters independently evaluating the quality of a signal, and then a third, more senior rater evaluates and clarifies any discrepancies between the two raters' ratings. The script outputs an event file that can be read back into BIOPAC and super-imposed on the original BIOPAC raw ECG data, using the native functionality for reading in events from Noldus Observer XT. This event file contains multiple different types of event labels, each prefaced with the partner role identifier ("P1", "P2"):
-"_Peak": an ECG R spike that both raters have agreed on
-"_Extra": an ECG R spike that one rater indicated, and the other did not
-"_Diff": an ECG R spike that both raters indicated, but for which there is substantial timing difference

### IBI FILTERING INPUT
This script requires the exact same type of BIOPAC journal file (see "Required File Format" for information on duping this format for other physiological recording programs) as the original individual primary rater files.

### IBI FILTERING OUTPUT
This script output a very similar, one-column data file containing the interbeat interval (IBI, or R-R interval) between each sequential ECG R spike pair. This format is suitable for being read directly into analyses requiring IBI data as the source, or into other programs that take IBI data and estimates other ECG metrics.

A good example of such an external program, for which these scripts were written, is Katie Gates's "RSASeconds" MATLAB program, which estimates an RSA time series from providied IBI data: http://gateslab.web.unc.edu/programs/rsaseconds/

### BIOPAC SPECIFIC DATA COLLECTION AND ANALYSIS INSTRUCTIONS
1. Data is recorded on a separate channel for each dyadic partner, with channel names constant across experimental dyads (so that the channel names can be used to identify each partner's ECG data).
2. Two different raters open the BIOPAC acquisition file (.acq) in BIOPAC AcqKnowledge and run the native ECG complex detection algorithm. They then correct R spike classification as needed.
3. Each rater exports their cleaned acquisition file journal as a .xls, which should then be converted to a .csv (easily accomplished with a free batch processor).

