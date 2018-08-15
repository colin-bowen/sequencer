# sequencer

function [sequence] = sequencer(x_intersects,y_intersects, start_index)
%sequencer pieces together vectors based on proximity. Cannot simply use
%sort because it is a spatial distribution, so must sort by geographic
%distance
%given the starting index of the sequencer, find the closest point to that
%point. Store the index of that point in the sequence of intersects. 
sequence = start_index; %initialize the index of points for the sequence.
x_intersects_orig = x_intersects;
while length(x_intersects) > 1
    start_x = x_intersects(start_index);
    start_y = y_intersects(start_index);
    x_intersects(start_index) = [];
    y_intersects(start_index) = [];
    min = 1000;
    for i = 1:length(x_intersects)
        test = sqrt((start_x - x_intersects(i))^2 + (start_y - y_intersects(i))^2);
        if test < min
            min = test;
            start_index = i;
            sequence_index = find(x_intersects_orig==x_intersects(i)); %store the index of the next point. 
        end
    end
    sequence = [sequence; sequence_index]; %append the index of the next point to the list. 
end

