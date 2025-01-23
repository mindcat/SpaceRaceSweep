## Software
### config.h
```c
#undef TAPPING_TERM
#define TAPPING_TERM 150

#define RETRO_SHIFT 500

#define USB_SUSPEND_WAKEUP_DELAY 0
#define AUTO_SHIFT_TIMEOUT 150
#define FORCE_NKRO 
#define COMBO_COUNT 3
#define HCS(report) host_consumer_send(record->event.pressed ? report : 0); return false
```
### rules.mk

```c
AUTO_SHIFT_ENABLE = yes
AUTO_SHIFT_MODIFIERS = yes
TAP_DANCE_ENABLE = yes
RETRO_SHIFT_ENABLE = yes
STENO_ENABLE = yes
STENO_PROTOCOL = geminipr
KEYBOARD_SHARED_EP = yes
COMBO_ENABLE = yes
LTO_ENABLE = yes
```

### keymap.c

```c
#include QMK_KEYBOARD_H
#include "quantum.h"
#include "keymap_steno.h"
#include "sendstring_colemak.h"

#define KC_MAC_UNDO LGUI(KC_Z)
#define KC_MAC_CUT LGUI(KC_X)
#define KC_MAC_COPY LGUI(KC_C)
#define KC_MAC_PASTE LGUI(KC_V)
#define KC_PC_UNDO LCTL(KC_Z)
#define KC_PC_CUT LCTL(KC_X)
#define KC_PC_COPY LCTL(KC_C)
#define KC_PC_PASTE LCTL(KC_V)
#define ES_LESS_MAC KC_GRAVE
#define ES_GRTR_MAC LSFT(KC_GRAVE)
#define ES_BSLS_MAC ALGR(KC_6)
#define NO_PIPE_ALT KC_GRAVE
#define NO_BSLS_ALT KC_EQUAL
#define LSA_T(kc) MT(MOD_LSFT | MOD_LALT, kc)
#define BP_NDSH_MAC ALGR(KC_8)
#define SE_SECT_MAC ALGR(KC_6)

enum custom_keycodes {
  ST_MACRO_0,
  MAC_MISSION_CONTROL,
  MAC_SPOTLIGHT,
  MAC_LOCK,
};

enum tap_dance_codes {
  DANCE_0,
  DANCE_1,
  DANCE_2,
  DANCE_3,
//   DANCE_4
};

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
  [0] = LAYOUT(
                                    
    KC_Q,           KC_W,           KC_F,           KC_P,           KC_B,                                           
    KC_J,           KC_L,           KC_U,           KC_Y,           KC_SCLN,      

    KC_A,           CTL_T(KC_R),    ALT_T(KC_S),    GUI_T(KC_T),    SFT_T(KC_G),                                                                           
    SFT_T(KC_M),    GUI_T(KC_N),    ALT_T(KC_E),    CTL_T(KC_I),    KC_O,           
    
    KC_X,           KC_C,           KC_D,           KC_V,           KC_Z,                                           
    KC_K,           KC_H,           KC_COMMA,       KC_DOT,         KC_SLASH,
                                                                                                    
    LT(1,KC_TAB),    LT(2,KC_SPACE),                      KC_BACKSPACE, KC_ENTER 
  ),
  [1] = LAYOUT(
                                                  
    KC_F1,          KC_F2,          KC_F3,          KC_F4,          KC_F5,                                            
    KC_F6,          KC_F7,          KC_F8,          KC_F9,          KC_F10,  

    KC_F11,         CTL_T(KC_F12),         ALT_T(KC_F3),          GUI_T(KC_F1),          KC_F2,                                                                    
    KC_NO,          GUI_T(KC_LEFT),        ALT_T(KC_DOWN),        CTL_T(KC_UP),          KC_RIGHT,

    KC_NO,          KC_NO,          KC_NO,          KC_NO,          KC_NO,                                   
    KC_NO,          KC_NO,          KC_NO,          KC_NO,          KC_NO,

    KC_NO, KC_NO,                KC_NO,    MAC_LOCK
  ),
  [2] = LAYOUT(

    TD(DANCE_0),    TD(DANCE_1),    TD(DANCE_2),    TD(DANCE_3),    KC_NO,
    KC_PLUS,        KC_7,           KC_8,           KC_9,           KC_ESC,

    KC_NO,          CTL_T(KC_GRAVE),  ALT_T(KC_QUOTE),  GUI_T(KC_EQUAL),     SFT_T(KC_NO),
    SFT_T(KC_MINUS),       GUI_T(KC_4),     ALT_T(KC_5),      CTL_T(KC_6),       KC_0,

    KC_NO,          ST_MACRO_0,     KC_SLASH,       KC_MINUS,       KC_NO,
    KC_DOT,         KC_1,           KC_2,           KC_3,           KC_BSLS,

    KC_TRNS,  KC_SPACE,        KC_BACKSPACE,   KC_NO
  ),
  [3] = LAYOUT(
                                                  
    KC_NO,          KC_NO,          KC_NO,          STN_N1,         KC_NO,                                            
    KC_NO,          STN_N2,         KC_NO,          KC_NO,          TO(0),           

    STN_S1,         STN_TL,         STN_PL,         STN_HL,         STN_ST1,                                                                          
    STN_DR,         STN_FR,         STN_PR,         STN_LR,         STN_TR,          

    STN_S2,         STN_KL,         STN_WL,         STN_RL,         STN_ST2,                                        
    STN_ZR,         STN_RR,         STN_BR,         STN_GR,         STN_SR,          
                                                                                                                
    STN_A,          STN_O,           STN_E,          STN_U
  ),
};

bool get_auto_shifted_key(uint16_t keycode, keyrecord_t *record) {
    // option 1
    if (IS_RETRO(keycode))1`;
        return true;

    // option 2
    switch (keycode) {
        // case QK_MOD_TAP ... QK_MOD_TAP_MAX:
        //     return true;
        case CTL_T(KC_R) || ALT_T(KC_S) || GUI_T(KC_T) || GUI_T(KC_N) || ALT_T(KC_E) || CTL_T(KC_I):
            return true;
        case KC_A ... KC_Z:
            return true;
        case KC_1 ... KC_0:
            return true;
        case KC_MINUS ... KC_SLASH:
            return true;
        default:
            return false;
    }
    
    return false;
}

const uint16_t PROGMEM combo0[] = { LT(1,KC_TAB), LT(2,KC_SPACE), COMBO_END};
const uint16_t PROGMEM combo1[] = { LT(1,KC_TAB), KC_BACKSPACE, COMBO_END};
const uint16_t PROGMEM combo2[] = { KC_A, KC_O, COMBO_END};

combo_t key_combos[COMBO_COUNT] = {
    COMBO(combo0, TO(3)),
    COMBO(combo1, LSFT(KC_TAB)),
    COMBO(combo2, KC_ESC)
};

bool process_record_user(uint16_t keycode, keyrecord_t *record) {
  switch (keycode) {
    case ST_MACRO_0:
      if (record->event.pressed) {
      //
      }
      else {
        // when keycode ST_MACRO_0 is released
        SEND_STRING("-> ");
      }
      break;
    case MAC_MISSION_CONTROL:
      HCS(0x29F);
    case MAC_SPOTLIGHT:
      HCS(0x221);
    case MAC_LOCK:
      HCS(0x19E);
  }
  return true;
}

typedef struct {
    bool is_press_action;
    uint8_t step;
} tap;

enum {
    SINGLE_TAP = 1,
    SINGLE_HOLD,
    DOUBLE_TAP,
    DOUBLE_HOLD,
    DOUBLE_SINGLE_TAP,
    MORE_TAPS
};

static tap dance_state[9];

uint8_t dance_step(tap_dance_state_t *state);

uint8_t dance_step(tap_dance_state_t *state) {
    if (state->count == 1) {
        if (state->interrupted || !state->pressed) return SINGLE_TAP;
        else return SINGLE_HOLD;
    } else if (state->count == 2) {
        if (state->interrupted) return DOUBLE_SINGLE_TAP;
        else if (state->pressed) return DOUBLE_HOLD;
        else return DOUBLE_TAP;
    }
    return MORE_TAPS;
}


void on_dance_0(tap_dance_state_t *state, void *user_data);
void dance_0_finished(tap_dance_state_t *state, void *user_data);
void dance_0_reset(tap_dance_state_t *state, void *user_data);

void on_dance_0(tap_dance_state_t *state, void *user_data) {
    if(state->count == 3) {
        tap_code16(KC_LABK);
        tap_code16(KC_LABK);
        tap_code16(KC_LABK);
    }
    if(state->count > 3) {
        tap_code16(KC_LABK);
    }
}

void dance_0_finished(tap_dance_state_t *state, void *user_data) {
    dance_state[0].step = dance_step(state);
    switch (dance_state[0].step) {
        case SINGLE_TAP: register_code16(KC_LABK); break;
        case SINGLE_HOLD: register_code16(KC_RABK); break;
        case DOUBLE_TAP: register_code16(KC_LABK); register_code16(KC_LABK); break;
        case DOUBLE_SINGLE_TAP: tap_code16(KC_LABK); register_code16(KC_LABK);
    }
}

void dance_0_reset(tap_dance_state_t *state, void *user_data) {
    wait_ms(10);
    switch (dance_state[0].step) {
        case SINGLE_TAP: unregister_code16(KC_LABK); break;
        case SINGLE_HOLD: unregister_code16(KC_RABK); break;
        case DOUBLE_TAP: unregister_code16(KC_LABK); break;
        case DOUBLE_SINGLE_TAP: unregister_code16(KC_LABK); break;
    }
    dance_state[0].step = 0;
}
void on_dance_1(tap_dance_state_t *state, void *user_data);
void dance_1_finished(tap_dance_state_t *state, void *user_data);
void dance_1_reset(tap_dance_state_t *state, void *user_data);

void on_dance_1(tap_dance_state_t *state, void *user_data) {
    if(state->count == 3) {
        tap_code16(KC_LCBR);
        tap_code16(KC_LCBR);
        tap_code16(KC_LCBR);
    }
    if(state->count > 3) {
        tap_code16(KC_LCBR);
    }
}

void dance_1_finished(tap_dance_state_t *state, void *user_data) {
    dance_state[1].step = dance_step(state);
    switch (dance_state[1].step) {
        case SINGLE_TAP: register_code16(KC_LCBR); break;
        case SINGLE_HOLD: register_code16(KC_RCBR); break;
        case DOUBLE_TAP: register_code16(KC_LCBR); register_code16(KC_LCBR); break;
        case DOUBLE_SINGLE_TAP: tap_code16(KC_LCBR); register_code16(KC_LCBR);
    }
}

void dance_1_reset(tap_dance_state_t *state, void *user_data) {
    wait_ms(10);
    switch (dance_state[1].step) {
        case SINGLE_TAP: unregister_code16(KC_LCBR); break;
        case SINGLE_HOLD: unregister_code16(KC_RCBR); break;
        case DOUBLE_TAP: unregister_code16(KC_LCBR); break;
        case DOUBLE_SINGLE_TAP: unregister_code16(KC_LCBR); break;
    }
    dance_state[1].step = 0;
}
void on_dance_2(tap_dance_state_t *state, void *user_data);
void dance_2_finished(tap_dance_state_t *state, void *user_data);
void dance_2_reset(tap_dance_state_t *state, void *user_data);

void on_dance_2(tap_dance_state_t *state, void *user_data) {
    if(state->count == 3) {
        tap_code16(KC_LBRC);
        tap_code16(KC_LBRC);
        tap_code16(KC_LBRC);
    }
    if(state->count > 3) {
        tap_code16(KC_LBRC);
    }
}

void dance_2_finished(tap_dance_state_t *state, void *user_data) {
    dance_state[2].step = dance_step(state);
    switch (dance_state[2].step) {
        case SINGLE_TAP: register_code16(KC_LBRC); break;
        case SINGLE_HOLD: register_code16(KC_RBRC); break;
        case DOUBLE_TAP: register_code16(KC_LBRC); register_code16(KC_LBRC); break;
        case DOUBLE_SINGLE_TAP: tap_code16(KC_LBRC); register_code16(KC_LBRC);
    }
}

void dance_2_reset(tap_dance_state_t *state, void *user_data) {
    wait_ms(10);
    switch (dance_state[2].step) {
        case SINGLE_TAP: unregister_code16(KC_LBRC); break;
        case SINGLE_HOLD: unregister_code16(KC_RBRC); break;
        case DOUBLE_TAP: unregister_code16(KC_LBRC); break;
        case DOUBLE_SINGLE_TAP: unregister_code16(KC_LBRC); break;
    }
    dance_state[2].step = 0;
}
void on_dance_3(tap_dance_state_t *state, void *user_data);
void dance_3_finished(tap_dance_state_t *state, void *user_data);
void dance_3_reset(tap_dance_state_t *state, void *user_data);

void on_dance_3(tap_dance_state_t *state, void *user_data) {
    if(state->count == 3) {
        tap_code16(KC_LPRN);
        tap_code16(KC_LPRN);
        tap_code16(KC_LPRN);
    }
    if(state->count > 3) {
        tap_code16(KC_LPRN);
    }
}

void dance_3_finished(tap_dance_state_t *state, void *user_data) {
    dance_state[3].step = dance_step(state);
    switch (dance_state[3].step) {
        case SINGLE_TAP: register_code16(KC_LPRN); break;
        case SINGLE_HOLD: register_code16(KC_RPRN); break;
        case DOUBLE_TAP: register_code16(KC_LPRN); register_code16(KC_LPRN); break;
        case DOUBLE_SINGLE_TAP: tap_code16(KC_LPRN); register_code16(KC_LPRN);
    }
}

void dance_3_reset(tap_dance_state_t *state, void *user_data) {
    wait_ms(10);
    switch (dance_state[3].step) {
        case SINGLE_TAP: unregister_code16(KC_LPRN); break;
        case SINGLE_HOLD: unregister_code16(KC_RPRN); break;
        case DOUBLE_TAP: unregister_code16(KC_LPRN); break;
        case DOUBLE_SINGLE_TAP: unregister_code16(KC_LPRN); break;
    }
    dance_state[3].step = 0;
}
tap_dance_action_t tap_dance_actions[] = {
        [DANCE_0] = ACTION_TAP_DANCE_FN_ADVANCED(on_dance_0, dance_0_finished, dance_0_reset),
        [DANCE_1] = ACTION_TAP_DANCE_FN_ADVANCED(on_dance_1, dance_1_finished, dance_1_reset),
        [DANCE_2] = ACTION_TAP_DANCE_FN_ADVANCED(on_dance_2, dance_2_finished, dance_2_reset),
        [DANCE_3] = ACTION_TAP_DANCE_FN_ADVANCED(on_dance_3, dance_3_finished, dance_3_reset),
};
```