---
title: "Standard sizes of rooms in flats"
date: 2023-03-29
draft: false
---

## Room Size Calculator

Use this interactive tool to determine if your room dimensions are small, medium, large, or luxury-sized, and see what furniture can comfortably fit in the space.

<div id="room-calculator">
  <h3>Room Size Calculator</h3>
  
  <div class="form-group">
    <label for="room-type">Room Type:</label>
    <select id="room-type">
      <option value="living">Living Room</option>
      <option value="bedroom">Bedroom</option>
      <option value="kitchen">Kitchen</option>
      <option value="dining">Dining Room</option>
      <option value="bathroom">Bathroom</option>
      <option value="balcony">Balcony</option>
    </select>
  </div>
  
  <div class="form-group">
    <label for="length">Length (in feet):</label>
    <input type="number" id="length" min="1" step="0.1">
  </div>
  
  <div class="form-group">
    <label for="width">Width (in feet):</label>
    <input type="number" id="width" min="1" step="0.1">
  </div>
  
  <button id="calculate-btn" class="room-calc-button">Calculate</button>
  
  <div id="results" style="display: none;">
    <h4>Results:</h4>
    <p id="area-result"></p>
    <p id="size-category"></p>
    <div id="furniture-fits"></div>
  </div>
</div>

<style>
  #room-calculator {
    background-color: #f5f5f5;
    padding: 20px;
    border-radius: 8px;
    max-width: 600px;
    margin: 20px auto;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  #room-calculator label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }
  
  #room-calculator input, #room-calculator select {
    width: 100%;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .room-calc-button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
  }
  
  .room-calc-button:hover {
    background-color: #45a049;
  }
  
  #results {
    margin-top: 20px;
    padding: 15px;
    background-color: #e8f5e9;
    border-radius: 4px;
  }
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const calculateBtn = document.getElementById('calculate-btn'); // Get the calculate button
  
  calculateBtn.addEventListener('click', function() {
    // Get input values
    const roomType = document.getElementById('room-type').value; // Get the selected room type
    const length = parseFloat(document.getElementById('length').value); // Get the length value
    const width = parseFloat(document.getElementById('width').value); // Get the width value
    
    // Validate inputs
    if (isNaN(length) || isNaN(width) || length <= 0 || width <= 0) {
      alert('Please enter valid dimensions'); // Show error if dimensions are invalid
      return;
    }
    
    // Calculate area
    const area = length * width; // Calculate the area of the room
    
    // Determine room size category and what can fit
    const result = evaluateRoomSize(roomType, length, width, area); // Evaluate the room size based on type and dimensions
    
    // Display results
    document.getElementById('area-result').textContent = `Room Area: ${area.toFixed(2)} sq ft`; // Display the calculated area
    document.getElementById('size-category').textContent = `Size Category: ${result.category}`; // Display the size category
    
    // Display furniture that can fit
    const furnitureDiv = document.getElementById('furniture-fits');
    furnitureDiv.innerHTML = '<h5>This room can accommodate:</h5>'; // Set heading for furniture list
    
    const furnitureList = document.createElement('ul'); // Create a list for furniture items
    result.furniture.forEach(item => {
      const listItem = document.createElement('li'); // Create a list item for each furniture piece
      listItem.textContent = item; // Set the text content of the list item
      furnitureList.appendChild(listItem); // Add the list item to the furniture list
    });
    
    furnitureDiv.appendChild(furnitureList); // Add the furniture list to the results div
    
    // Show results
    document.getElementById('results').style.display = 'block'; // Make the results visible
  });
  
  // Function to evaluate room size based on type and dimensions
  function evaluateRoomSize(roomType, length, width, area) {
    let category = '';
    let furniture = [];
    
    // Evaluate based on room type
    switch(roomType) {
      case 'living':
        if (area < 120) {
          category = 'Small Living Room';
          furniture = [
            '2-seater sofa or 2 armchairs',
            'Small coffee table',
            'TV unit with up to 32" TV',
            'Limited circulation space'
          ];
        } else if (area < 180) {
          category = 'Small Living Room';
          furniture = [
            '3-seater sofa',
            'Coffee table',
            'TV unit with 40" TV',
            'Limited circulation space',
            'Best for 2-3 people gathering'
          ];
        } else if (area < 270) {
          category = 'Medium Living Room';
          furniture = [
            '3-seater sofa',
            '1-seater armchair',
            'Coffee table',
            'TV unit with 50" TV',
            'Side table',
            'Comfortable circulation space',
            'Suitable for 4-5 people gathering'
          ];
        } else if (area < 432) {
          category = 'Large Living Room';
          furniture = [
            'L-shaped sofa or 3-seater + 2-seater combination',
            'Coffee table',
            'TV unit with 55"-65" TV',
            'Side tables',
            'Bookshelf',
            'Generous circulation space',
            'Can accommodate 6-8 people comfortably'
          ];
        } else {
          category = 'Luxury Living Room';
          furniture = [
            'Complete sofa set (3+2+1)',
            'Coffee table',
            'Large TV unit',
            'Bookshelves',
            'Display cabinets',
            'Dining area',
            'Abundant circulation space',
            'Perfect for entertaining large groups of 10+ people'
          ];
        }
        break;
        
      case 'bedroom':
        if (area < 80) {
          category = 'Small Bedroom';
          furniture = [
            'Single bed',
            'Small wardrobe',
            'Bedside table',
            'Limited circulation space',
            'Best for children or single adults'
          ];
        } else if (area < 120) {
          category = 'Medium Bedroom';
          furniture = [
            'Double bed',
            '2-door wardrobe',
            'One or two bedside tables',
            'Adequate circulation space',
            'Comfortable for a single person or couple'
          ];
        } else if (area < 180) {
          category = 'Large Bedroom';
          furniture = [
            'Queen or king-sized bed',
            'Large wardrobe or walk-in closet',
            'Two bedside tables',
            'Dresser or vanity',
            'Seating area with chair',
            'Comfortable circulation space',
            'Suitable for master bedroom'
          ];
        } else {
          category = 'Luxury Bedroom';
          furniture = [
            'King-sized bed',
            'Walk-in closet',
            'Full bedroom set with bedside tables',
            'Dresser and vanity',
            'Seating area with chairs or chaise lounge',
            'TV unit',
            'Workspace or desk',
            'Generous circulation space',
            'Perfect for luxury master suites'
          ];
        }
        break;
        
      case 'kitchen':
        if (area < 50) {
          category = 'Small Kitchen';
          furniture = [
            'Single counter with sink',
            'Compact refrigerator',
            '2-burner stove',
            'Limited cabinet space',
            'Minimal circulation space',
            'Best for single-person households'
          ];
        } else if (area < 80) {
          category = 'Medium Kitchen';
          furniture = [
            'L-shaped counter with sink',
            'Standard refrigerator',
            '4-burner stove',
            'Adequate cabinets',
            'Sufficient circulation space for one person',
            'Suitable for small families or couples'
          ];
        } else if (area < 120) {
          category = 'Large Kitchen';
          furniture = [
            'U-shaped or L-shaped counter with island',
            'Full-sized refrigerator',
            'Cooking range',
            'Dishwasher',
            'Ample cabinets',
            'Comfortable circulation space for multiple people',
            'Can accommodate a family with cooking enthusiasts'
          ];
        } else {
          category = 'Luxury Kitchen';
          furniture = [
            'Multiple work zones',
            'Large island',
            'Full-sized appliances',
            'Pantry space',
            'Extensive cabinetry',
            'Generous circulation space for multiple cooks',
            'Perfect for entertaining and gourmet cooking'
          ];
        }
        break;
        
      case 'dining':
        if (area < 64) {
          category = 'Small Dining Area';
          furniture = [
            'Small round or square table for 2-4 people',
            'Minimal circulation space',
            'Best for apartments or small households',
            'Often part of an open-plan kitchen/living area'
          ];
        } else if (area < 100) {
          category = 'Medium Dining Room';
          furniture = [
            'Rectangular table for 4-6 people',
            'Sufficient circulation space',
            'Suitable for small families or couples who occasionally entertain',
            'May accommodate a small sideboard or buffet'
          ];
        } else if (area < 168) {
          category = 'Large Dining Room';
          furniture = [
            'Large rectangular table for 6-8 people',
            'Sideboard or buffet',
            'Comfortable circulation space',
            'Can accommodate family gatherings and dinner parties',
            'Space for additional furniture like china cabinets'
          ];
        } else {
          category = 'Formal Dining Room';
          furniture = [
            'Extended dining table for 8-12 people',
            'Buffet',
            'China cabinet',
            'Serving table',
            'Generous circulation space for serving and movement',
            'Perfect for entertaining and formal dining occasions',
            'May include space for a bar area or additional seating'
          ];
        }
        break;
        
      case 'bathroom':
        if (area < 18) {
          category = 'Very Small Bathroom';
          furniture = [
            'Toilet',
            'Small sink',
            'Very limited circulation space',
            'Functional but tight'
          ];
        } else if (area < 40) {
          category = 'Small Powder Room';
          furniture = [
            'Toilet and small sink',
            'Minimal circulation space',
            'Best for guest bathrooms or half baths',
            'No bathing facilities'
          ];
        } else if (area < 64) {
          category = 'Small Full Bathroom';
          furniture = [
            'Toilet',
            'Sink',
            'Shower or tub',
            'Limited circulation space',
            'Common in apartments and smaller homes',
            'Efficient layout with fixtures along walls'
          ];
        } else if (area < 100) {
          category = 'Medium Bathroom';
          furniture = [
            'Toilet',
            'Vanity sink',
            'Tub/shower combination',
            'Adequate circulation space',
            'May include small storage cabinet',
            'Comfortable for daily use'
          ];
        } else if (area < 144) {
          category = 'Large Bathroom';
          furniture = [
            'Toilet',
            'Double vanity',
            'Separate tub and shower',
            'Comfortable circulation space',
            'Room for storage cabinets or linen closet',
            'Suitable for master bathrooms'
          ];
        } else {
          category = 'Luxury Bathroom';
          furniture = [
            'Toilet (possibly in separate water closet)',
            'Double vanity',
            'Soaking tub',
            'Walk-in shower',
            'Generous circulation space',
            'Ample storage options',
            'May include seating area or dressing space',
            'Perfect for spa-like master bathrooms'
          ];
        }
        break;
        
      case 'balcony':
        if (area < 12) {
          category = 'Juliet Balcony';
          furniture = [
            'Standing space only with protective railing',
            'Primarily decorative with minimal usable space',
            'Provides ventilation but limited utility'
          ];
        } else if (area < 24) {
          category = 'Small Utility Balcony';
          furniture = [
            'Small plants',
            'Limited standing space',
            'Functional for essential outdoor needs'
          ];
        } else if (area < 40) {
          category = 'Utility Balcony';
          furniture = [
            'Clothes drying area',
            'Small plants',
            'Functional space for essential outdoor needs',
            'Common in mid-range apartments',
            'Often attached to kitchen or utility areas'
          ];
        } else if (area < 60) {
          category = 'Standard Balcony';
          furniture = [
            '2-chair seating arrangement',
            'Several potted plants',
            'Comfortable for 1-2 people to sit',
            'Typical in most modern apartments',
            'Versatile for multiple uses'
          ];
        } else if (area < 96) {
          category = 'Large Balcony';
          furniture = [
            'Small table with 2-4 chairs',
            'Multiple plants',
            'Comfortable for family seating',
            'Found in premium apartments',
            'Can be used as an outdoor dining area'
          ];
        } else {
          category = 'Luxury Terrace Balcony';
          furniture = [
            'Lounge furniture',
            'Dining set',
            'Extensive plants/garden',
            'Spacious enough for entertaining guests',
            'Available in high-end apartments and penthouses',
            'Can be designed as an outdoor living room'
          ];
        }
        break;
    }
    
    return {
      category: category,
      furniture: furniture
    };
  }
});
</script>

## Introduction

In India, room measurements are typically expressed in feet (ft). One foot is approximately equal to the length of an adult human foot (about 30.48 centimeters or 12 inches). This unit of measurement has historical roots and remains the standard for real estate and construction in India despite the country's official adoption of the metric system.

## Drawing rooms/Living rooms

### Common Furniture Dimensions

Living rooms typically need to accommodate various furniture pieces. Here are standard dimensions of common items:

- **Sofas**:

  - 1-seater sofa/armchair: 2.5 ft × 3 ft (width × depth)
  - 2-seater sofa: 4 ft × 3 ft
  - 3-seater sofa: 6 ft × 3 ft
  - L-shaped sofa: 8 ft × 6 ft (typical configuration)

- **Tables**:
  - Center/coffee table: 3 ft × 1.5 ft
  - Side table: 1.5 ft × 1.5 ft
  - TV unit: 4-6 ft × 1.5 ft

### Standard Living Room Sizes and What They Can Accommodate

#### Small Living Room (10 ft × 12 ft = 120 sq ft)

- Can fit: 3-seater sofa, coffee table, TV unit with 40" TV
- Limited circulation space
- Best for 2-3 people gathering

#### Medium Living Room (12 ft × 15 ft = 180 sq ft)

- Can fit: 3-seater sofa, 1-seater armchair, coffee table, TV unit with 50" TV, side table
- Comfortable circulation space
- Suitable for 4-5 people gathering

#### Large Living Room (15 ft × 18 ft = 270 sq ft)

- Can fit: L-shaped sofa or 3-seater + 2-seater combination, coffee table, TV unit with 55"-65" TV, side tables, bookshelf
- Generous circulation space
- Can accommodate 6-8 people comfortably

#### Luxury Living Room (18 ft × 24 ft = 432 sq ft)

- Can fit: Complete sofa set (3+2+1), coffee table, large TV unit, bookshelves, display cabinets, dining area
- Abundant circulation space
- Perfect for entertaining large groups of 10+ people

## Bedrooms

### Common Furniture Dimensions

Bedrooms need to accommodate essential furniture pieces. Here are standard dimensions of common items:

- **Beds**:

  - Single bed: 3 ft × 6.5 ft (width × length)
  - Double bed: 4.5 ft × 6.5 ft
  - Queen size bed: 5 ft × 6.5 ft
  - King size bed: 6 ft × 6.5 ft

- **Storage**:
  - Wardrobe (2-door): 4 ft × 1.5 ft (width × depth)
  - Wardrobe (3-door): 6 ft × 1.5 ft
  - Dresser with mirror: 3 ft × 1.5 ft
  - Bedside table: 1.5 ft × 1.5 ft

### Standard Bedroom Sizes and What They Can Accommodate

#### Small Bedroom (8 ft × 10 ft = 80 sq ft)

- Can fit: Single bed, small wardrobe, bedside table
- Limited circulation space
- Best for a single person or child's room

#### Medium Bedroom (10 ft × 12 ft = 120 sq ft)

- Can fit: Double bed, 2-door wardrobe, bedside table, small desk
- Adequate circulation space
- Suitable for a couple or single person with more storage needs

#### Large Bedroom (12 ft × 14 ft = 168 sq ft)

- Can fit: Queen size bed, 3-door wardrobe, two bedside tables, dresser
- Comfortable circulation space
- Can accommodate a couple with ample storage and movement space

#### Master Bedroom (14 ft × 16 ft = 224 sq ft)

- Can fit: King size bed, large wardrobe, two bedside tables, dresser, seating area
- Generous circulation space
- Perfect for a primary bedroom with attached bathroom

## Kitchens

### Common Kitchen Elements Dimensions

Kitchens need to accommodate essential fixtures and appliances. Here are standard dimensions of common items:

- **Countertops and Work Surfaces**:

  - Standard counter depth: 2 ft (24 inches)
  - Standard counter height: 3 ft (36 inches)
  - Minimum counter length per function: 2 ft (24 inches)

- **Appliances**:

  - Refrigerator: 2.5-3 ft × 2.5 ft (width × depth)
  - Cooking range/stove: 2 ft × 2 ft
  - Microwave: 1.5 ft × 1.3 ft
  - Dishwasher: 2 ft × 2 ft

- **Storage**:
  - Upper cabinet depth: 1 ft
  - Lower cabinet depth: 2 ft
  - Standard cabinet height: 2.5 ft (30 inches)

### Standard Kitchen Sizes and What They Can Accommodate

#### Small Kitchen (7 ft × 8 ft = 56 sq ft)

- Can fit: Single counter with sink, compact refrigerator, 2-burner stove, limited cabinets
- Minimal circulation space
- Best for studio apartments or single-person households

#### Medium Kitchen (8 ft × 10 ft = 80 sq ft)

- Can fit: L-shaped counter with sink, standard refrigerator, 4-burner stove, adequate cabinets
- Sufficient circulation space for one person
- Suitable for small families or couples

#### Large Kitchen (10 ft × 12 ft = 120 sq ft)

- Can fit: U-shaped or L-shaped counter with island, full-sized refrigerator, cooking range, dishwasher, ample cabinets
- Comfortable circulation space for multiple people
- Can accommodate a family with cooking enthusiasts

#### Luxury Kitchen (12 ft × 15 ft = 180 sq ft or larger)

- Can fit: Multiple work zones, large island, full-sized appliances, pantry space, extensive cabinetry
- Generous circulation space for multiple cooks
- Perfect for entertaining and gourmet cooking

## Dining Rooms

### Common Dining Room Elements Dimensions

Dining rooms need to accommodate tables, chairs, and circulation space. Here are standard dimensions of common items:

- **Dining Tables**:

  - Small round table (2-4 people): 3-4 ft diameter
  - Rectangular table (4-6 people): 5 ft × 3 ft
  - Large rectangular table (6-8 people): 7 ft × 3.5 ft
  - Extension tables can add 1-2 ft when expanded

- **Seating**:

  - Standard chair width: 1.5-2 ft
  - Space needed per seated person: 2 ft width
  - Clearance behind chairs: 2.5-3 ft for comfortable movement

- **Circulation**:
  - Minimum passage around table with seated guests: 2.5 ft
  - Comfortable passage: 3-4 ft

### Standard Dining Room Sizes and What They Can Accommodate

#### Small Dining Area (8 ft × 8 ft = 64 sq ft)

- Can fit: Small round or square table for 2-4 people
- Minimal circulation space
- Best for apartments or small households
- Often part of an open-plan kitchen/living area

#### Medium Dining Room (10 ft × 10 ft = 100 sq ft)

- Can fit: Rectangular table for 4-6 people
- Sufficient circulation space
- Suitable for small families or couples who occasionally entertain
- May accommodate a small sideboard or buffet

#### Large Dining Room (12 ft × 14 ft = 168 sq ft)

- Can fit: Large rectangular table for 6-8 people, sideboard or buffet
- Comfortable circulation space
- Can accommodate family gatherings and dinner parties
- Space for additional furniture like china cabinets

#### Formal Dining Room (14 ft × 16 ft = 224 sq ft or larger)

- Can fit: Extended dining table for 8-12 people, buffet, china cabinet, serving table
- Generous circulation space for serving and movement
- Perfect for entertaining and formal dining occasions
- May include space for a bar area or additional seating

## Bathrooms

### Common Bathroom Elements Dimensions

Bathrooms need to accommodate fixtures, storage, and movement space. Here are standard dimensions of common bathroom elements:

- **Fixtures**:

  - Standard toilet: 2.5 ft × 1.5 ft
  - Pedestal sink: 1.5-2 ft width
  - Vanity sink: 2-3 ft width
  - Standard bathtub: 5 ft × 2.5 ft
  - Shower stall: 3 ft × 3 ft (minimum)
  - Combination tub/shower: 5 ft × 2.5-3 ft

- **Clearances**:

  - Front of toilet: 2 ft minimum
  - Side of toilet: 1.5 ft minimum from center
  - Front of sink: 2 ft minimum
  - Front of shower/tub: 2-2.5 ft minimum

- **Circulation**:
  - Minimum passage width: 2 ft
  - Comfortable passage: 2.5-3 ft

### Standard Bathroom Sizes and What They Can Accommodate

#### Small Powder Room (3 ft × 6 ft = 18 sq ft)

- Can fit: Toilet and small sink
- Minimal circulation space
- Best for guest bathrooms or half baths
- No bathing facilities

#### Small Full Bathroom (5 ft × 8 ft = 40 sq ft)

- Can fit: Toilet, sink, and shower or tub
- Limited circulation space
- Common in apartments and smaller homes
- Efficient layout with fixtures along walls

#### Medium Bathroom (8 ft × 8 ft = 64 sq ft)

- Can fit: Toilet, vanity sink, and tub/shower combination
- Adequate circulation space
- May include small storage cabinet
- Comfortable for daily use

#### Large Bathroom (10 ft × 10 ft = 100 sq ft)

- Can fit: Toilet, double vanity, separate tub and shower
- Comfortable circulation space
- Room for storage cabinets or linen closet
- Suitable for master bathrooms

#### Luxury Bathroom (12 ft × 12 ft = 144 sq ft or larger)

- Can fit: Toilet (possibly in separate water closet), double vanity, soaking tub, walk-in shower
- Generous circulation space
- Ample storage options
- May include seating area or dressing space
- Perfect for spa-like master bathrooms

## Balconies

Balconies are important outdoor spaces in Indian homes that provide fresh air, natural light, and additional living area. Here are the standard sizes and considerations for balconies in Indian flats:

### Balcony Dimensions and Considerations

- **Minimum Width**: 3 ft (0.9 m) is the absolute minimum, but 4-5 ft (1.2-1.5 m) is more functional
- **Depth**: Typically ranges from 3-8 ft (0.9-2.4 m) depending on apartment size and type
- **Railing Height**: Minimum 3.5 ft (1.1 m) for safety as per most building codes
- **Door Width**: Standard 2.5-3 ft (0.75-0.9 m) for access

### Standard Balcony Types and Sizes in Indian Apartments

#### Juliet Balcony (2-3 ft × 3-4 ft = 6-12 sq ft)

- Primarily decorative with minimal usable space
- Allows for standing only with protective railing
- Common in budget apartments and smaller flats
- Provides ventilation but limited utility

#### Utility Balcony (4 ft × 6 ft = 24 sq ft)

- Can fit: Clothes drying area, small plants
- Functional space for essential outdoor needs
- Common in mid-range apartments
- Often attached to kitchen or utility areas

#### Standard Balcony (5 ft × 8 ft = 40 sq ft)

- Can fit: 2-chair seating arrangement, several potted plants
- Comfortable for 1-2 people to sit
- Typical in most modern apartments
- Versatile for multiple uses

#### Large Balcony (6 ft × 10 ft = 60 sq ft)

- Can fit: Small table with 2-4 chairs, multiple plants
- Comfortable for family seating
- Found in premium apartments
- Can be used as an outdoor dining area

#### Luxury Terrace Balcony (8 ft × 12 ft = 96 sq ft or larger)

- Can fit: Lounge furniture, dining set, extensive plants/garden
- Spacious enough for entertaining guests
- Available in high-end apartments and penthouses
- Can be designed as an outdoor living room

## Now lets take example of 1 BHK flat

![1 BHK Flat](/images/2.jpg)

Let's analyze this 1 BHK flat layout, examining each room's practicality based on the provided dimensions:

1. **Living Room (13'0" × 9'7")**

   - What's shown: Main living space
   - Practicality: At approximately 125 sq ft, this is slightly larger than our defined "Small Living Room"
   - Can realistically fit: 3-seater sofa, coffee table, TV unit, and possibly a compact dining arrangement
   - Assessment: Adequate for a small family or couple with reasonable circulation space

2. **Kitchen (6'10" × 9'9")**

   - What's shown: Rectangular kitchen
   - Practicality: At about 67 sq ft, this is a medium-sized kitchen
   - Can fit: Standard refrigerator, 3-burner stove, sink, and moderate counter space
   - Assessment: Comfortable for daily cooking needs with space for basic appliances

3. **Bedroom (9'0" × 10'0")**

   - What's shown: Single bedroom
   - Practicality: At 90 sq ft, falls between our "Small Bedroom" and "Medium Bedroom" categories
   - Can fit: Double bed, 2-door wardrobe, and one bedside table
   - Assessment: Adequate for a single person or couple with modest storage needs

4. **Cupboard Space (6'10" × 2'0")**

   - What's shown: Dedicated storage area
   - Practicality: At about 14 sq ft, provides valuable additional storage
   - Assessment: Useful feature that compensates for limited storage in other areas

5. **Toilet 1 (4'1" × 5'1")**

   - What's shown: Primary bathroom
   - Practicality: At about 21 sq ft, this is a compact bathroom
   - Assessment: Functional but tight; can accommodate standard fixtures with minimal circulation space

6. **Toilet 2 (4'6" × 3'4")**

   - What's shown: Secondary bathroom
   - Practicality: At about 15 sq ft, this is a very compact bathroom
   - Assessment: Likely designed as a powder room or guest toilet with minimal fixtures

7. **Dry Balcony (3'5" × 6'10")**

   - What's shown: Utility outdoor space
   - Practicality: At about 23 sq ft, this qualifies as a "Utility Balcony"
   - Can fit: Washing machine and clothes drying arrangement
   - Assessment: Functional for essential utility needs but limited for other uses

8. **Living Balcony (7'0" × 5'0")**
   - What's shown: Main balcony off living area
   - Practicality: At 35 sq ft, this falls between our "Utility Balcony" and "Standard Balcony" categories
   - Can fit: 2-chair seating arrangement and several potted plants
   - Assessment: Provides a reasonable outdoor extension to the living space

For a single person or minimalist couple, this layout works adequately. However, families or those requiring more spacious living conditions would likely find this arrangement restrictive for long-term comfort.

For a video tour of this 1 BHK flat layout, you can watch the walkthrough below:

<div style="text-align: center;"> <!-- Center align the video -->
    <iframe width="560" height="315" src="https://www.youtube.com/embed/GSZ9kXbnX8I?si=ZXcUUsMvkqUQRUxR" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div> <!-- End of center alignment -->
